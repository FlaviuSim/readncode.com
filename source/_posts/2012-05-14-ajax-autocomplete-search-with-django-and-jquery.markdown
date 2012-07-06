---
layout: post
title: "AJAX Autocomplete Search with Django and jQuery"
date: 2012-02-27
comments: true
categories: Django Programming Python
permalink: /blog/AJAX-Autocomplete-Search-with-Django-and-jQuery
---

Let's say you have some data that you want to autocomplete in a text field as the user types.

This is what your Django model might look like if you were searching for drug names:

```python
from django.db import models
class Drug(model.Model):
    rxcui = models.IntegerField()
    short_name = models.CharField(max_length=50)
    is_brand = models.IntegerField(max_length=1)
```

It's very likely that your data is in a different format (csv or pipe delimited), like this:

```
Rxcui|Short Name|Is Brand
1234 |Advil     |1
```

So we need to import that data. A database copy command (postgres, mysql, sqlite) will not deal very nicely with our Django auto-incrementing keys, so we need to add the data using a django view, such as this:

```python
import csv
from myproject.main.models import Drug
def load_drugs(file_path):
    "this loads drugs from pipe delimited file with headers"
    reader = csv.DictReader(open(file_path))
    for row in reader:
        drug = Drug(rxcui=row['Rxcui'], short_name=row['Short Name'], is_brand=row['Is Brand'])
        drug.save()
```

Now load the django console and import the data:

```bash
$ python manage.py shell
$ from main.view import load_drugs
$ load_drugs('/absolute/path/to/pipe/file.txt')
```

Cool. Now we need to actually write the template where the search is. We'll use [jQuery Autocomplete](http://jqueryui.com/demos/autocomplete/) because that's what the cool kids do. Let's first import jQuery and jQueryUI in our base template:

```html
<link rel="stylesheet" href="http://code.jquery.com/ui/1.8.18/themes/base/jquery-ui.css" type="text/css" media="all" />
<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js" type="text/javascript">
</script> <script src="https://ajax.googleapis.com/ajax/libs/jqueryui/1.8.16/jquery-ui.min.js" type="text/javascript"></script>
```

Now let's add this to the template we want the search field on:

```html
<div class="ui-widget">
  <label for="drugs">Drugs: </label>
  <input id="drugs">
</div>
```

Our own javascript to get the autocomplete is this (you can put it anywhere after the jQuery imports):

```javascript
$(function() {
  $("#drugs").autocomplete({
    source: "/api/get_drugs/",
    minLength: 2,
  });
});
```

Where is the ajax call happening? jQuery Autocomplete does it for us. But how does it know which fields to get? It doesn't! Let's implement the url:

```python
url(r'^api/get_drugs/', 'myproject.main.view.get_drugs', name='get_drugs'),
```

And now,the real work. Our view:

```python
def get_drugs(request):
    if request.is_ajax():
        q = request.GET.get('term', '')
        drugs = Drug.objects.filter(short_name__icontains = q )[:20]
        results = []
        for drug in drugs:
            drug_json = {}
            drug_json['id'] = drug.rxcui
            drug_json['label'] = drug.short_name
            drug_json['value'] = drug.short_name
            results.append(drug_json)
        data = json.dumps(results)
    else:
        data = 'fail'
    mimetype = 'application/json'
    return HttpResponse(data, mimetype)
```

Note that jQuery autocomplete sends the query as "term" and it expects back three fields: id, label, and value. It will use those to display the label and then the value to autocomplete each drug.

We now have an AJAX jQuery Autocomplete Search with Django. Hope this helps.

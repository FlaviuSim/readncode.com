---
layout: post
title: "Max Field Length from a Data File"
date: 2012-02-29
comments: true
categories: Programming Python
permalink: /blog/max-field-length-from-data-file
---

Sometimes you have a .csv or a pipe delimited file that you need to insert into a database. You need to create the table using SQL and you're not sure whether to use VARCHAR(40) or VARCHAR(100). 

If only you could quickly tell what the longest field for each column was...

Here's a script to do that:

```python
import csv, sys

lengths = {}

with open(sys.argv[1], 'rt') as f:
    reader = csv.DictReader(f, delimiter='|') #pipe separated
    for index, row in enumerate(reader):
        if index == 0:
            for heading in row.keys():
                lengths[heading] = 0 #set the dict headings
        for column in row.keys():
            if (len(row[column]) > lengths[column]):
                lengths[column] = len(row[column]) #add length
    print lengths
```

Then, just run it from the command line:

```bash
$ python longest_field.py random_file.txt
```

Hope this helps.

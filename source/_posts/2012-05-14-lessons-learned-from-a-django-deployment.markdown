---
layout: post
title: "Lessons Learned from a Django Deployment"
date: 2011-01-21
comments: true
permalink: /blog/lessons-learned-from-a-django-deployment
categories: Django Programming Python
---

This website was built with Django 1.2.4, and is hosted by <a
href="http://webfaction.com">Webfaction.com</a>. Webfaction is easy to
set up, and if you are not a deployment expert (i.e. you are not Jacob
Kaplan-Moss) that's what you should use.

I followed James Bennet's book some of the way. It has a few errors in
the code and it is a little dated, but it helped me as a beginner. You
can find it <a
href="http://www.amazon.com/Practical-Django-Projects-Pratical/dp/1590599969/ref=sr_1_1?ie=UTF8&s=books&qid=1295650150&sr=8-1">here</a>.

<strong>Use django-taggit</strong>

<a
href="http://www.google.com/url?sa=t&source=web&cd=1&ved=0CBsQFjAA&url=http%3A%2F%2Fcode.google.com%2Fp%2Fdjango-tagging%2F&ei=ow46Tae6EcP88AaoquCyCg&usg=AFQjCNGIEdldVWgClxnLXaHC9Poabhpglw&sig2=WJPIhH0CrDIPCeQ_J1zPHQ">django-tagging</a>
is kind of dead, and <a href="http://alexgaynor.net">Alex Gaynor</a>
(who is probably the most productive programmer who can't buy alcohol
legally in the US) has made a better and more extensible alternative: <a
href="https://github.com/alex/django-taggit">django-taggit</a>. It
actually has a couple of extensions and it's on Eric Holscher's Read the
Docs <a
href="http://readthedocs.org/projects/alex/django-taggit/">here</a>.

<strong>Pay attention to which Python Version you are using</strong>

Webfaction (like just about every computer) has multiple versions of
python installed, and one (usually not the one you want) will be used
when you type "python" To use the one you want, say 2.6, you either type
"python2.6" every time, or you add this line to your ~/.bash_profile
(create it if it's not there):


```bash
alias python=python2.6
```

Some use ~/.profile or ~/.bashrc instead. Read more about the difference
(or lack thereof) <a
href="http://stefaanlippens.net/bashrc_and_others">here</a>. Also, make
sure that you use the right version of the python packages you install.
You may think you are installing something with pip and then you can't
import it because you should have installed it with pip for that version
of python: pip-2.6

<strong>render_to_response() does not have the Request Context by
default</strong>

I had a simple app that had mostly generic views. Naturally, I used 
MEDIA_URL for all my links to media. But on some pages, no media
showed up. A few mental hours later, I figured out that generic views
include the Request Context by default, whereas render_to_response does
not. So, I had to write:

```python
return render_to_response('template.html', { 'dictionary' : dictionary }, context_instance = RequestContext(request))
```

That's it for now. Overall, deployment was a good
experience.

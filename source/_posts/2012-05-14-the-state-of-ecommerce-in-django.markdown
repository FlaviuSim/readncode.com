---
layout: post
title: "The state of eCommerce in Django"
date: 2011-04-18
comments: true
categories: Django Python
permalink: /blog/the-state-of-ecommerce-in-django
---

So, you're looking for a reusable, extendable, pony-powered eCommerce
app?

Here's what's out there:

<p></p>
[Satchmo](http://www.satchmoproject.com/)
-------
Most well known. Huge, does everything you and your brother could ever
want, but the client, that's another story. 

So, you're in the code, and hours go by because the Product
[models.py](https://bitbucket.org/chris1610/satchmo/src/4dcd30f11ad7/satchmo/apps/product/models.py)
has 1570 lines and it turns out it was a problem with
**PriceAdjustmentCalc**, whatever that does.

<p></p>
[Lightning Fast Shop](http://www.getlfs.com/)
---------

Full blown solution (like satchmo), with batteries included, docs,
tests, demo, and a lot of code. So regardless whether you need it or
not, you get it all. And then, if you need something different, you'll
have to **ack** and **grep** a bit.

<p></p>
[Satchless](http://satchless.com/)
-------------------------

Still in early development, but very straightforward and well documented
so far. Actively developed and a good starting point for most use cases.
Very pluggable and customizable products, categories and variants. 

Same dude also made [mamona](https://github.com/emesik/mamona), which is
a nice payment abstraction mechanism.

<p></p>
[Plata](https://github.com/matthiask/plata)
-----------------------------

Made by the [FeinCMS](http://www.feinheit.ch/media/labs/feincms/)
people. A pretty solid, simple, pluggable alternative for a "shop."
docs, tests, nice code. It makes you write your own urls and views by
leveraging some of the model interface it has. 

The examples are pretty simple and only offer a product list and detail.
I think doing more complex things will require a bunch of code, and the
framework doesn't seem to do much to make that process easier for you.

<p></p>
[Cartridge](http://cartridge.jupo.org/)
-----------------------

Pretty nice, but a plugin for [mezzanine](http://mezzanine.jupo.org/),
to which it's tightly coupled. So, more code to sift through. Yes! Also,
not very modular, with long functions, though it's no satchmo.

<p></p>
[django-shop](https://github.com/divio/django-shop)
-----------------------

Made by the [django-cms](https://www.django-cms.org/) guys. 1.3 ready.
Good intentions, no real example, or tests. 
EDIT: It does have
[tests](https://github.com/divio/django-shop/tree/master/shop/tests) and
a [simple
example](https://github.com/divio/django-shop/tree/master/example). See
comments below.

Simple products you can subclass. You can add a plugin for variants, and
I am guessing categories. Fairly straightforward, but perhaps a bit
simplistic, which is... meh.

<p></p>
[gnocchi-catalogue](https://bitbucket.org/funkybob/gnocchi-catalogue/)
------------------------------------------

Early stage, no docs, no tests, pretty solid first attempt, bitbucket :(

<p></p>
[rollyourown_commerce](http://readthedocs.org/projects/roll-your-own/)
-----------------------------------

Easy to set up, but lacks the complexity of categories and variants, or
the abstraction of common functionality most options above offer.

For me it would be between [Satchless](http://satchless.com/) and
[Plata](https://github.com/matthiask/plata), and I would choose
[Satchless](http://satchless.com/) because it seems like the project I
would enjoy contributing to the most.


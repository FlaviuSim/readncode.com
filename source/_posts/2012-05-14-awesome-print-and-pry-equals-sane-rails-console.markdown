---
layout: post
title: "awesome_print and Pry = Sane Rails Console"
date: 2011-12-01
comments: true
categories: Programming Rails
permalink: /blog/awesome-print-and-pry-sane-rails-console
---

{% img http://readncode.com/media/images/blog/awesome-print.png %}

I recently found out about [awesome_print](https://github.com/michaeldv/awesome_print) so I gave it a try.

It lets you print objects very nicely, like the adjacent image shows.

Moreover, I am already using [pry](http://pry.github.com/).

So, I can type something like this in the Rails console to print all the users:

```bash
cd User
all
```

Combining these two gems, I can now get the output in the image above like this:

```bash
cd Survey
ap first;
```

The beauty of this made me want to blog it. That is all.

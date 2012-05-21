---
layout: post
title: "Why ack can't find some queries"
date: 2012-01-18
comments: true
categories: Programming
permalink: /blog/why-ack-cant-find-some-queries
---

{% img http://readncode.com/media/images/blog/ack.png %}

**[Ack](http://betterthangrep.com/)** often regains the attention of [HackerNews](http://news.ycombinator.com/item?id=975511) for being better than **grep**. They're not shy either: the ack home page is [betterthangrep.com](http://betterthangrep.com/).

I've been using ack for a few months, and while it's awesome, sometimes it can't find some stuff that I know is in my project. This upsets me.

Come to find out, part of the reason ack is so fast is that it skips certain files (finally read some docs). Most importantly, **it skips any file it doesn't recognize.**

So, basically, my *.haml*, *.scss*, and *.coffee* files are not searched by default.

To find out which file types it does search, just type:

```bash
ack --help=types
```

I can either add some command line argument to include those files (which I don't remember),  add a -a flag to search everything, or create a **.ackrc** file in your home folder. 

I opted for the latter:

~/.ackrc
```bash
--type-set
haml=.haml
--type-set
sass=.sass,.scss
--type-set
coffee=.coffee
```

Now those files are searched too. Hope this helps another Flaviu out there.

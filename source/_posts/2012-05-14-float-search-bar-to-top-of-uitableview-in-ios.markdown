---
layout: post
title: "Float Search Bar to Top of UITableView in iOS"
date: 2012-03-28
comments: true
categories: Objective-C Programming
permalink: /blog/float-search-bar-to-top-of-uitableview-in-ios
---

{% img http://readncode.com/media/images/blog/ipad_search.png %}


Don't you wish you could scroll in the image above and keep the search bar floating at the top?

Two steps: 

**Uno.** Add the UIScrollViewDelegate protocol to your interface:

<p></p>
<script src="https://gist.github.com/2226884.js?file=gistfile1.m"></script>

**Dos.** Implement the scrollViewDidScroll protocol method:

<p></p>
<script src="https://gist.github.com/2226909.js?file=gistfile1.m"></script>

Done. So easy.

But I kind of also want the search text field to be larger (increase its height). How hard can that be?

Well, as it turns out, pretty hard. After spending 1+ hour researching posts like [this one](http://stackoverflow.com/questions/556814/changing-the-size-of-the-uisearchbar-textfield/556935), I gave up. I guess it looks OK the way Steve Jobs designed it.

Welcome to iOS.


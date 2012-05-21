---
layout: post
title: "Search for a package using apt-get"
date: 2012-01-27
comments: true
categories: Programming
permalink: /blog/search-for-a-package-using-apt-get
---

I can't tell you how many times I've typed:

```bash
$ apt-get search git
E: Invalid operation search 
```

unlike *brew search*, *gem search*, *npm search* and every other packaging, **[APT](http://en.wikipedia.org/wiki/Advanced_Packaging_Tool)** decided to use a different prefix:

```bash
apt-cache search git
```

I'm not even going to ask why **git** is under **git-core**.

---
layout: post
title: "iOS Chart and Plotting Library Comparison"
date: 2012-05-15 15:36
author: Flaviu Simihaian
comments: true
categories:  Objective-C Programming
---

tl;dr:
-----
Use [core-plot](http://code.google.com/p/core-plot/), roll your own CoreGraphics implementation, or use a WebView with a JavaScript plotting library, such as [Highcharts](http://www.highcharts.com/) or [FusionCharts](http://www.fusioncharts.com/)

{% img no-box center http://www.shinobicontrols.com/media/1555/charts_banner_image.png %}

I needed to chart some data for an iPad app. Here's some options I've
found in my research:

I looked on StackOverflow but there was no clear winner:
[http://stackoverflow.com/questions/7254882/line-graphs-on-ios](http://stackoverflow.com/questions/7254882/line-graphs-on-ios)

Some suggested writing your own with CoreGraphics; some mentioned ShinobiControls, but it costs like  $1,000 and doesn't look all that great:
[http://www.shinobicontrols.com/shinobicharts/price-plans/](http://www.shinobicontrols.com/shinobicharts/price-plans/)

Core Plot
--------

This is what most people suggest. It does apparently anything you want. But it's on Google Code and the documentation is awful.

[http://code.google.com/p/core-plot/](http://code.google.com/p/core-plot/)

Unofficial Github Mirror: [https://github.com/djw/core-plot](https://github.com/djw/core-plot)

Sencha
------

If you're not doing native work, I should mention Sencha has some pretty
nice looking stuff: 
[http://dev.sencha.com/deploy/touch-charts-1.0.0/examples/](http://dev.sencha.com/deploy/touch-charts-1.0.0/examples/)

However, I am only building native apps, so it doesn't help me that
much.

Lameness
--------

Then there's tons of lame sites last updated in 2010 that you should stay away from:
[http://www.keepedge.com/products/iphone_charting/](http://www.keepedge.com/products/iphone_charting/)
[http://www.iphonechart.com/company/](http://www.iphonechart.com/company/)

JavaScript
----------

I ended up using a JavaScript framework instead and build a WebView
locally using that library. It's worked out pretty well:

{% img center http://cl.ly/GioX/Screen%20Shot%202012-05-18%20at%2011.22.55%20AM.png %}

I used [FusionCharts](http://www.fusioncharts.com/), but I've also used [Highcharts](http://www.highcharts.com/) before and liked it even more. However, FusionCharts has [a nice tutorial](http://blog.fusioncharts.com/2012/02/create-charts-for-iphone-and-ipad-apps-using-fusioncharts-xt/) for how to embed it inside an iOS app.

Or you could use [Google Charts](https://developers.google.com/chart/).

That ended up working great for the quick nice chart I needed. Hope this helps you. If you've used other tools, please let me know by commenting below.


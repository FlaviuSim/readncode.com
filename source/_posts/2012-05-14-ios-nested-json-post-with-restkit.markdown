---
layout: post
title: "iOS: Nested JSON POST with RestKit"
date: 2012-04-25
comments: true
categories: Objective-C Programming
permalink: /blog/ios-nested-json-post-with-restkit
---

Say you want to send some JSON from your RestKit enabled iOS app. You want your JSON to look like this:

<p></p>
<script src="https://gist.github.com/2492208.js?file=gistfile1.html"></script>

First, make the corresponding NSDictionary structure:

<p></p>
<script src="https://gist.github.com/2492223.js?file=gistfile1.m"></script>

Then, create the JSON string from your NSDictionary

<p></p>
<script src="https://gist.github.com/2492231.js?file=gistfile1.j"></script>

Finally, make the request and map the response to a model:

<p></p>
<script src="https://gist.github.com/2492237.js?file=gistfile1.m"></script>

Hope this helps.

---
layout: post
title: "How to write a multi-line NSString in Objective-C"
date: 2012-06-26 22:19
comments: true
categories: Objective-C Programming
---

Say you have some HTML you need to cram into a WebView in iOS. You can create a
.html file but then you can't pass variables from your code.

So, you try inlining it. Except you find out that Objective-C does not
have like a triple quote or some other multi-line escaping.

You need to end every line with a backslash. So, this code:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>U.S. Population</title>
    <script type="text/javascript" src="../../d3.v2.js"></script>
    <link type="text/css" rel="stylesheet" href="population.css"/>
  </head>
  <body>
    <div id="chart"></div>
    <script type="text/javascript" src="population.js"></script>
  </body>
</html>
```

needs to become this:

```objc
@" \
<!DOCTYPE html> \
<html> \
<head> \
<title>U.S. Population</title> \
<script type=\"text/javascript\" src=\"d3.v2.min.js\"></script> \
<link type=\"text/css\" rel=\"stylesheet\" href=\"population.css\"/> \
</head> \
<body> \
<div id=\"chart\"></div> \
<script type=\"text/javascript\" src=\"population.js\"></script> \
</body> \
</html> \
"
```

You don't want to do that manually. So I made a little tool that converts one to the other. Check it out at [MultiLineObjC.herokuapp.com](http://multilineobjc.herokuapp.com/).

Hope this saves you some time.

---
layout: post
title: "Nil and Zero in Ruby and Objective-C"
date: 2012-01-26
comments: true
categories: Programming
permalink: /blog/nil-and-zero-in-ruby-and-objective-c
---

{% img http://readncode.com/media/images/blog/nil.jpg %}

In Ruby, only **nil** and **false** are treated as **false**. Everything else is **true**.

Yes, that includes **0**. The following statement will evaluate as true:

```ruby
puts "Waat?" if 0
```

So to check if something is nil you can use one of these methods:

```ruby
puts "Waaat?" if defined?(wat_object)
puts "Waaat?" unless wat_object.nil?
```

Or, if you need to initialize an instance variable that you never want to be nil, here's the sexiness to use:

```ruby
 @wat_variable ||= "Waaat?"
```

This will check if the variable is nil, and if so, assign it to "Waaat?". Otherwise, it will leave it untouched.

Objective-C uses **YES** and **NO** or non-zero and **0** instead of **true** and **false**. An object pointer that does not point to anything is **nil**.

```objc
NSString *hello = nil;
```

**nil** is the exact same as **0**. **nil** is used for objects, while **0** for primitive types (int, double, etc). 

**Both *nil* and *0* evaluate to false in Objective C**, so both of these print statements would not execute.

```objc
id obj = nil;
int some_int = 0;
if (obj) { print "waaat?"; }
if(some_int) { print "waaat?"; }
```

I often get confused about whether nil is true or false, so I hope this helps somebody.



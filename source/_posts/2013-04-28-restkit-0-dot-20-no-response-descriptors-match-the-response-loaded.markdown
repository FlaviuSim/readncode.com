---
layout: post
title: "RestKit 0.20 : No response descriptors match the response loaded"
date: 2013-04-28 19:41
comments: true
categories: Objective-C Programming
---

{% img center http://i.qkme.me/3u58sy.jpg %}

Well, as the error message in XCode and as Blake Water explains in [this github issue](https://github.com/RestKit/RestKit/issues/1060) the paths don't match.

It's especially subtle when you have a get parameter, like I did:

```objc
NSString *resourcePath = [NSString stringWithFormat:@"/counties_by_zip/?zipcode=%@", zipCode];
RKResponseDescriptor *responseDescriptor = [RKResponseDescriptor responseDescriptorWithMapping:[MappingProvider zipMapping] pathPattern:resourcePath keyPath:nil statusCodes:RKStatusCodeIndexSetForClass(RKStatusCodeClassSuccessful)];
```

 It turns out that if you have a parameter like that, your path
 needs to NOT include it, like so:

```objc
RKResponseDescriptor *responseDescriptor = [RKResponseDescriptor responseDescriptorWithMapping:[MappingProvider zipMapping] pathPattern:@"/counties_by_zip/" keyPath:nil statusCodes:RKStatusCodeIndexSetForClass(RKStatusCodeClassSuccessful)]; 
```

 That's it folks. 2 hours of my time. It's yours.

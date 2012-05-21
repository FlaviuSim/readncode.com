---
layout: post
title: "Seeding CoreData with RestKit"
date: 2012-04-05
comments: true
categories: Objective-C Programming
permalink: /blog/Seeding-CoreData-with-RestKit
---

{% img http://cl.ly/Fb2d/Screen%20Shot%202012-04-05%20at%201.54.47%20PM.png %}

I've recently written [a post](http://readncode.com/blog/Load-SQLite-db-into-Core-Data-in-iOS-5/) about seeding your SQLite database into Core Data.

Fortunately, [@SteveMoser](https://twitter.com/#!/SteveMoser) pointed out I should be using [RestKit](http://restkit.org/).

RestKit includes a Restful HTTP Client, Object Mapping, and a bunch of other stuff, like Database Seeding. Big monsters typically scare me, but I gave it a try because I really needed a better way to seed my data.

First thing's first: you need to set up RestKit for your project. I won't go into the details, because they are [here](https://github.com/RestKit/RestKit/wiki/Installing-RestKit-in-Xcode-4.x).

Once RestKit is installed, here's what you need to do to seed your database from JSON:

I. Create a new target for your application. Call it "Generate Seed" or something.

The way to create a new target is to click on your project, and in the "Summary", click on Add Target:

<img src="http://cl.ly/Fb3O/Screen%20Shot%202012-04-05%20at%202.09.37%20PM.png" />

II. Click on the newly created target, go to "Build Settings" and search for "macros". Double click on the value for "Preprocessor Macros" and overwrite whatever is in there with "RESTKIT_GENERATE_SEED_DB" (without the quotes, obviously). Click Done.

III. Now we need to modify out AppDelegate.m a bit. First, import the RestKit.h and RestKit's CoreData:

```objc
#import <RestKit/RestKit.h>
#import <RestKit/CoreData.h>
```

Here's what your appFinishLaunchingWithOptions might look like (this is  mostly from RestKit's example Twitter project):

<p></p>
<script src="https://gist.github.com/2313087.js?file=gistfile1.m"></script>

IV. The data we're seeding will need to be in JSON. So, in our case, I dragged a statuses.json file in XCode and copied it there (make sure it's in the Seed Target, as we have no use for it in our main Target).

But what is in that JSON file?

Basically this:

```
[{
"id":213,
"created_at":"Sat Mar 05 13:39:09 +0000 2011",
"text":"Meaningful tweet about Nihilism"
},
{
"id":214,
"created_at":"Sat Mar 06 13:39:09 +0000 2011",
"text":"Letdown tweet after the last retwat"
}]
```

RestKit uses the mappings in the code above to map each JSON field to your CoreData model. Then there's a little more ceremony, and we're done.

Not really. We haven't run it yet.

V. To generate the seed database, you'll want to run the seed target we created. You do that by clicking on the top left between the stop button and the device you select. Run it in the simulator, not on the device. 

<img src="http://cl.ly/FauR/Screen%20Shot%202012-04-05%20at%202.35.53%20PM.png" />

When you build your code, you may get some weird Mach-O Linker errors like this:

<img src="http://cl.ly/FXQz/Screen%20Shot%202012-04-02%20at%207.22.26%20PM.png" />

Best thing I've found was to delete the seed target and recreate it.

If that doesn't work, you may try manually deleting the Seed Database and CoreData database in the file system.

After it runs successfully, it will print in the console a message to copy the sqlite seed database it just generated to your project. Open that folder in the Finder and drop it in your project.

You should now be able to run your main target and the seed data will be there.

Next time you change your model or seed data, you just need to delete the Seed App from your simulator, run the seed target again, and copy the seed database it creates to your project.


Hope this helps. mobile tuts+ also has a [nice tutorial](http://mobile.tutsplus.com/tutorials/iphone/advanced-restkit-development_iphone-sdk/) that might help with some of this stuff.

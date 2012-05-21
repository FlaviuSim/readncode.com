---
layout: post
title: "Load SQLite db into Core Data in iOS 5"
date: 2012-03-01
comments: true
categories: Objective-C Programming
permalink: /blog/Load-SQLite-db-into-Core-Data-in-iOS-5
---

*UPDATE: I've tried using [RestKit](http://restkit.org) to seed my db and it's much easier. I wrote [a blog post](http://readncode.com/blog/Seeding-CoreData-with-RestKit/) about it if you're interested.*

Many Model-View-Controller frameworks have a way to specify seed data (initial data for an application to function).

iOS does not. So we have to create another app that builds the database, and then have the main app copy that database and set it as default when the app first loads.

Let's create that new app and call it UtilityApp and make sure it has the same Core Data Model as our main app:

<img style="margin-top: 20px" src="http://cl.ly/Eda9/Screen%20Shot%202012-03-01%20at%207.15.23%20AM.png" />

Copy the SQLite database (which you want to use to populate our Core Data) in the "Supporting Files" in XCode:

<img style="margin-top: 20px" src="http://cl.ly/EeAx/Screen%20Shot%202012-03-01%20at%207.03.41%20AM.png" />

Now either in your AppDelegate.m or in a new class, you need to populate your Core Data with the sqlite database data. I made a class called DrugFetcher.h with a public method: 

```objc
+ (void) populateDrugsInManagedObjectContext:(NSManagedObjectContext *)context;
```

We need to import sqlite3:

```
#import "/usr/include/sqlite3.h"
```

However, to have access to that, we need to add it from the "Build Phases" tab of our project: 

<img style="margin-top: 20px" src="http://cl.ly/Eddv/Screen%20Shot%202012-03-01%20at%207.07.31%20AM.png" />

Here's my DrugFetcher.m

<script src="https://gist.github.com/1949450.js"> </script>

The script above opens the SQLite db, and adds each row to a model.

Now the "seed" database is prepared. We need get it from the UtilityApp and add it to our main app's resources. You can run the Utility app on your desktop and then find the path where your Application is running and copy the db from there.

I prefer to ssh into the device just for my peace of mind that it was created on the target device. You'll need to jailbreak your device to ssh into it, a process which I covered [here](http://readncode.com/blog/how-to-ssh-into-your-ios-device/).

To copy the file you run something like this on your device:

```bash
scp /var/mobile/Applications/LONG-APP-CODE-FROM-DEBUGGER/Documents/StoreContent/persistentStore user@your_machine:~/path/to/app/
```

On your computer, I recommend opening the 'persistentStore' with sqlite3 and making sure there are no extra tables, and delete all the contents of the Z_METADATA table. I've run into issues with this before.

```bash
$ sqlite3 persistentStore
delete * from Z_METADDATA;
```

Add the persistentStore (a SQLite db) to the main app Supporting Files. 

<img style="margin-top: 20px" src="http://cl.ly/EeHI/Screen%20Shot%202012-03-01%20at%207.23.14%20AM.png" />

Now, in your main app, you'll want to change your AppDelegate a bit to make sure it uses the new db. If it's the first time the app is loaded, it will copy the persistentStore to Documents/CoreDataStore.sqlite. From then on, it will use CoreDataStore.sqlite as its data store.

We'll use NSPersistentStoreCoordinator to achieve this. Here's my AppDelegate.h:

<script src="https://gist.github.com/1949516.js"> </script>

The copying on first load is achieved in the persistentStoreCoordinator method, like so:

<script src="https://gist.github.com/1949656.js"> </script>

Then, in the same persistentStoreCoordinator method, we add our new store to the persistentStoreCoordinator:

<script src="https://gist.github.com/1949661.js"> </script>

Here's the full AppDelegate.m for reference:

<script src="https://gist.github.com/1949538.js"> </script>

I realize this gets confusing, so ask questions below. I've wasted plenty of my time loading data, so maybe this post saves some of yours.

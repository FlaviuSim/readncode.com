---
layout: post
title: "How to SSH into your iOS device over WiFi and 3G"
date: 2012-01-25
comments: true
categories: Hacking Life
permalink: /blog/how-to-ssh-into-your-ios-device
---

{% img http://readncode.com/media/images/blog/iPhone-iPad-A5-ssh.png %}

The latest iHipster devices are now jailbreak-able using **[this Absinthe tutorial](http://www.redmondpie.com/jailbreak-5.0.1-ios-untethered-iphone-4s-ipad-2-using-absinthe-how-to-video-tutorial/)** from [RedmondPie](http://www.redmondpie.com/).

One of the things you should get from Cydia (after MyWi, SBSettings, and VLC), is OpenSSH to let you SSH into your device and do things such as copy movies for **[VLC](http://www.videolan.org/vlc/)** to play.

After you get OpenSSH, you'll notice that nothing happens. Don't worry, it's running.

To connect to it you'll need the device's IP Address which, if you are on a WiFi network, you can go to Settings->Wi-Fi and click on the name of the Wi-Fi to see the IP Address. 

Then type this into your computer Terminal:

```bash
ssh root@ip_address_you_just_found
```

Your password will initially be *alpine* but the first thing you should do is change it, like so:

```bash
passwd
New Password: Enter_super_secret_password_you_ruski
```

Now you are free. (as in speech)

If you are on 3G, you'll need Reverse SSH Tunneling set up, which isn't as glorious as its name:

Get the *pTerm* app or some other Terminal app for iOS (either from the App Store or from the forbidden Installous garden).

Type this to set up the tunneling:

```bash
ssh -R 19999:localhost:22 computer_user@computer_ip
```

You need to keep that connection (and app) open from your iOS device with the *Backgrounder* App, which will be a battery hog.

On your computer you can now connect with this command:

```bash
ssh root@localhost -p 19999
```

Again, the WiFi option is the way to go, but if you must connect to it via 3G, you can do so as well.

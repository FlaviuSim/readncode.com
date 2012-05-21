---
layout: post
title: "How to dismiss popovers in iOS"
date: 2012-02-12
comments: true
categories: Objective-C Programming
permalink: /blog/how-to-dismiss-popovers-in-ios
---

{% img no-box http://readncode.com/media/images/blog/popover.png %}

I wanted a quick edit field to display in a popover in an iPad app and then click done to have the popup disappear.Pretty standard, right?

8 hours later I was able to replicate the functionality. I hope these tips save you some time:

**1:** With XCode 4.2, you get Storyboards, which allow you to visually create a segue by right-clicking from the Button to the view you want to display. Use them.

If you click on the segue, you'll have to give it a name and choose the Style (in our case, **Popover**).

[Scott Sherwood](http://www.scott-sherwood.com/?p=219) has a great article on using Storyboards in Xcode 4.2.

**2:**  Keep a reference to the segue before the segue is made.

```objc 
(void)prepareForSegue:(UIStoryboardPopoverSegue *)segue sender:(id)sender{
    if([[segue identifier] isEqualToString:@"EditFilterSegue"]){
        editPopover = [(UIStoryboardPopoverSegue *)segue popoverController];
        editPopover.delegate = (id <UIPopoverControllerDelegate>)self;
    }
}
```

Thanks to [Symmetric on stackoverflow](http://stackoverflow.com/questions/8225589/ios-create-an-popover-view-using-storyboard) for the code above. 

**3:**  Dismissing the popover needs to happen in the delegate (the controller that put that popover on screen).

You may be tempted to write something like this:

```objc 
-(void)dismissPopover:(id)sender
{
  [self dismissViewControllerAnimated:YES completion:NULL]; 
//or better yet
  [self dismissModalViewControllerAnimated:YES]; 
//the latter works fine for Modal segues
}
```

The code you want is this:

```objc 
-(void)dismissPopover:(id)sender
{
    [editPopover dismissPopoverAnimated:YES];
}
```

However, what the hell is that **editPopover** I keep having in my code? That is the variable we need to have to keep track of the popover (**though it seems like only a select few know this**)

So, in your delegate header file define it:

```objc 
@interface PatientTableViewController : CoreDataTableViewController {
    UIPopoverController *createPatientPopover;
}
```

Don't worry about making it a property, synthesizing it, and all that jazz.

**4:** Yay! The popover **Done** button now works. Wait a minute, if you tap it multiple times, it creates multiple popovers...and then it won't dismiss all of them. Wat?

Since you don't want to ship with that weirdness, we need to keep track of the Done button with some more variables on our @interface:

```objc 
    id createSender;
    id createTarget;
    SEL createAction;
```

Then, we want to add these lines to our *prepareForSegue*:

```objc 
        // Save the done button's info so we can restore it
        createAction = [sender action];
        createTarget = [sender target];
        createSender = sender;
        // Change the done button's target to us, and its action to dismiss the popover
        [sender setAction:@selector(dismissPopover:)];
        [sender setTarget:self];
```

And, add these lines to our *dismissPopover*:

```objc 
-(void)dismissPopover:(id)sender
{
    [createSender setAction:createAction];
    [createSender setTarget:createTarget];
    [createPatientPopover dismissPopoverAnimated:YES];
}
```

And, if someone taps outside of the popover to dismiss it, it should act the same way:

```objc 
-(BOOL)popoverControllerShouldDismissPopover:(UIPopoverController *)popoverController
{
    [createSender setAction:createAction];
    [createSender setTarget:createTarget];
    return YES;
}
```



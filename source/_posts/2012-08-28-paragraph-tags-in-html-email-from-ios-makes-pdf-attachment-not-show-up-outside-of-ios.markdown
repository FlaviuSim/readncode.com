---
layout: post
title: "Paragraph Tags in HTML email from iOS makes PDF attachment not show up outside of iOS"
date: 2012-08-28 18:50
comments: true
categories:  Objective-C Programming
---

Here's a standard way to send an HTML email with a PDF attachment from
iOS:

```objc
// add the attachment
[mailComposer addAttachmentData:myData mimeType:@"application/pdf" fileName:@"comparison.pdf"];

// Fill out the email body text
NSString *emailBody = @" \
<p>Bla bla bla.</p>\
\
<p>See comparison attached.</p> \
";

[mailComposer setMessageBody:emailBody isHTML:YES];
[self presentModalViewController:mailComposer animated:YES];
```

You will be happy when checking the result of this on your iOS device.
However, when you check it in Gmail, it looks like this:

{% img center http://cl.ly/J3uZ/Screen%20Shot%202012-08-28%20at%207.25.30%20PM.png %}

What? Why? I don't know!! What I do know is that it works if you put **br** tags instead:

```objc
// Fill out the email body text
NSString *emailBody = @" \
Bla bla bla.<br /><br />\
\
See comparison attached. \
";
```

Now it looks as it should:

{% img center http://cl.ly/J4Gq/Screen%20Shot%202012-08-28%20at%207.28.34%20PM.png %}

So, the lesson is: WTF?!

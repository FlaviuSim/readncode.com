---
layout: post
title: "How to send user signup notifications to Campfire from Rails"
date: 2011-09-13
comments: true
categories: Rails
permalink: /blog/user-notifications-from-campfire-to-rails
---

<p>Let's say you have a user signup page, and you want to be notified whenever a user signs up in the Campfire chat.</p>

**[tinder](https://github.com/collectiveidea/tinder/)** is the best library to interface with the Campfire API. I know that because it was last released today. So, gem install tinder.

Then, open your user.rb file and add the following:

```ruby
after_save :announce_signup
```

```ruby
def announce_signup
    campfire = Tinder::Campfire.new 'yoursubdomain', :token => 'your_token_here'
    room = campfire.find_room_by_id(enter_room_id)
     room.speak "#{name} signed up!"
end
```

<p>The first line makes sure the announcement happens only after save.</p>

Then, we initiate the connection to Campfire using **tinder** and our subdomain, key, and room id. The **speak** function assumes your User model has a **name** attribute, which would be printed in the Campfire chat.

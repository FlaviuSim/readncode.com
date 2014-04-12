---
layout: post
title: "Create New Records with Bootstrap Modal and Rails Unobtrusive Javascript"
date: 2012-05-28 19:36
comments: true
categories: Rails Frontend Programming
---

{% img http://cl.ly/GxW1/Screen%20Shot%202012-05-28%20at%209.10.25%20PM.png %}

I wanted the quickest way to get a nice looking modal popover, in which to
create a new record, and after the modal dismisses, the new record to
show up. All without the page refreshing. 

And let's throw in validations in the modal as well.

Say you have a simple model (Post) with some fields.
``` bash
rails new flapp
cd flapp
rails g scaffold Post title content
```

Add [client_side_validations](https://github.com/bcardarella/client_side_validations) to take care of validations for us (only gem we're going to use, I promise...except haml-rails so you can actually read HTML)
``` ruby Gemfile
gem 'client_side_validations'
```

Run the install generator for client_side_validations
``` bash
rails g client_side_validations:install
```

Add the rails.validations.js to your layout
``` js app/assets/javascripts/application.js
//= require rails.validations
```

Now, we need to download Bootstrap. I recommend customizing it with the cool things you want on [this page](http://twitter.github.com/bootstrap/download.html). If that fails, the minified full version is only 48k. Make sure you copy the javascripts, css, and images into your assets directory accordingly.

We'll just edit 'app/views/posts/index.html.haml' for this example so that it's all in one file. However, it's good practice to render each modal in a different file.

Change your 'Add Post' button to this:
``` haml posts/index.html.haml
%a{'href' => '#new-post-modal', 'data-toggle' => 'modal'}
```

The **data-toggle** tells Bootstrap this link toggles the modal. The **href** tells it the ID of the modal element it toggles.

Here's our modal:

``` haml app/views/posts/index.html.haml
#new-post-modal{'class' => 'modal hide fade'}
  = form_for(Post.new, validate: true, remote: true, html: {"data-type" => :json}) do |f|
    %ul.errors
      %li
    .field
      = f.label :title
      = f.text_field :title
    .field
      = f.label :content
      = f.text_field :content
    .actions
      = f.submit 'Save'
```

The ```validate: true``` makes sure we use the client_side_validations we added earlier. ```remote: true``` tells it to use [Rails' Unobtrusive Javascript](https://github.com/rails/jquery-ujs).

The ```html: {"data-type" => :json})``` specifies that we want the controller to return JSON back to the view.

The classes (modal, hide, fade) declare it as a modal that is hidden at first, and then fades in.

With the latest Rails, we don't need to change anything in the controller. Here's what my create action looks like:

```ruby app/controllers/posts_controller.rb
def create
  @post = Post.new(params[:post])

  respond_to do |format|
    if @post.save
      format.html { redirect_to @post, notice: 'Post was successfully created.' }
      format.json { render json: @post, status: :created, location: @post }
    else
      format.html { render action: "new" }
      format.json { render json: @post.errors, status: :unprocessable_entity }
    end
  end
end
```

The only thing we need to do is to make sure we are listening for when the JSON comes back, so that we can dismiss the modal, and show the new data.

``` coffeescript app/assets/javascripts/posts.js.coffee
$ ()->
  $("form.new_post").on "ajax:success", (event, data, status, xhr) ->
    $('#new-post-modal').modal('hide')
    $('table tbody').append('<tr><td>' + data.title + '</td><td>' + data.content + '</td></tr>')
```

In the case above, we dismiss the modal and then insert a new row in a table with the title and content of the post we just added.

I tried to keep this as simple as possible. Hope it helps.

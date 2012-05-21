---
layout: post
title: "Get the model in a fields_for block"
date: 2011-11-05
comments: true
categories: Programming Rails
permalink: /blog/Get-the-model-in-a-fields_for-block
---

I have a fields_for block in my view, like this:

```ruby
    = form_survey.fields_for :questions, (@survey.questions) do  |form_questions|
```

But I want to access each question model directly within the block. I tried **question** or **@question** and after endless searches, I found the **object** attribute:

```ruby
form_questions.object
```

which contains all this awesome:

```ruby
--- !ruby/ActiveRecord:Question 
    attributes: 
      id: "65"
      survey_id: "42"
      text: "0"
      created_at: 2011-11-03 18:24:02.746409
      updated_at: 2011-11-03 18:24:02.746409
      position: "0"
      question_type: SINGLE
```

Yes! I hope this saves another Flaviu some time.

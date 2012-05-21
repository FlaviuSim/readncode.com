---
layout: post
title: "factory_girl association validation problems"
date: 2011-09-17
comments: true
categories: Rails
permalink: /blog/factory-girl-association-validation
---

You want to test if a foreign key exists (Question belongs_to Survey). Of course you use [factory_girl](https://github.com/thoughtbot/factory_girl).

You might approach it the way I have below, but then you get the error at the end, that makes absolutely no sense:
<p></p>
<script src="https://gist.github.com/1224087.js?file=gistfile1.rb"></script>

You might read that there is a difference between :create and :build and that's the problem, so you change the survey association line to something like this:
<p></p>
<script src="https://gist.github.com/1224294.js?file=gistfile1.rb"></script>

But what's really the problem?

Despite the rspec error, the problem is in the Survey factory definition, which has an after_build callback to generate a couple of questions every time it builds a survey:
<p></p>
<script src="https://gist.github.com/1224293.js?file=gistfile1.rb"></script>

Factory_girl does not like this recursiveness, and so you should take it out. Once you do, it all works.

If anyone has a better solution to this, please comment below.

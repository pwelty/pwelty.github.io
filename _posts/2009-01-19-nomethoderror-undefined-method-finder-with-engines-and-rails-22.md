---
id: 13
title: 'NoMethodError (undefined method `finder&#8217;) with Engines and Rails 2.2'
date: 2009-01-19T16:01:32-04:00
author: paul
layout: post
guid: http://www.paulwelty.com/?p=13
permalink: /ruby-on-rails/nomethoderror-undefined-method-finder-with-engines-and-rails-22/
categories:
  - Ruby on Rails
---
I was getting this error with Rails 2.2 when using ActionMailer.

NoMethodError (undefined method \`finder&#8217; for #<ActionView::Base:0x34146fc>)

It stems from a line in engines/lib/engines/rails\_extensions/action\_mailer.rb

This is some problem between Rails 2.2 and Engines. Reinstalling engines didn&#8217;t seem to help.

Simply put, you need to go here and apply this patch:

http://github.com/lazyatom/engines/commit/499ce3b0480d8fa9375203f5efcadb8cf6ea9efe

This took me hours to figure out. I don&#8217;t know why there isn&#8217;t any more help on this problem.
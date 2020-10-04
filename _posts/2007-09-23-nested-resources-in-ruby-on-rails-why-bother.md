---
id: 7
title: 'Nested resources in Ruby on Rails: why bother?'
date: 2007-09-23T19:11:03-04:00
author: paul
layout: post
guid: http://www.paulwelty.com/ruby-on-rails/nested-resources-in-ruby-on-rails-why-bother/
permalink: /ruby-on-rails/nested-resources-in-ruby-on-rails-why-bother/
categories:
  - Ruby on Rails
---
Nested resources in Ruby on Rails are sort of neat, but they are a pain to implement. What&#8217;s more, I have to ask myself, why bother?

If a resource has a unique identifier id, then why would you need to call its parent resource to call it? The unique identifier is enough. And what resource doesn&#8217;t have a unique id these days?
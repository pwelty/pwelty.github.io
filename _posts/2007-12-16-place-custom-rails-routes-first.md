---
id: 10
title: Place Custom Rails Routes First
date: 2007-12-16T08:44:40-04:00
author: paul
layout: post
guid: http://www.paulwelty.com/ruby-on-rails/place-custom-rails-routes-first/
permalink: /ruby-on-rails/place-custom-rails-routes-first/
categories:
  - Ruby on Rails
---
This is another one that should have been obvious. But, I was getting it wrong. Maybe it had something to do with upgrading to Rails 1.2.6.

Anyway, I was getting an error with a custom action. I was sending a form to &#8220;projects/do\_something&#8221;. But, I kept getting the error of &#8220;Can&#8217;t find project with ID=do\_something&#8221;.

This was happening because Rails thought it was supposed to be looking in the route for the show action. But, checking the routes file, I could see that I had defined my custom route. What, what was up?

It turns out, the custom route has to come before the standard &#8220;map.resources :projects&#8221; line.

Once I fixed that, all is well again. (I still think this acted differently in 1.2.3. Hmm).
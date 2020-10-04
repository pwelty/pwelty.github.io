---
id: 12
title: 'Rails + SugarCRM &#8211; An alternative approach'
date: 2008-01-11T09:39:13-04:00
author: paul
layout: post
guid: http://www.paulwelty.com/ruby-on-rails/rails-sugarcrm-an-alternative-approach/
permalink: /ruby-on-rails/rails-sugarcrm-an-alternative-approach/
categories:
  - Ruby on Rails
---
After slogging through connecting Rails and Sugar via SOAP, I was tired and frustrated. The API is slow, and doing anything meaningful took a long time (ok, it took 30 seconds, but that seems slow to me; aren&#8217;t computers supposed to be fast?!). So, I came up with an alternative approach.

I know that Active Record (or whatever it&#8217;s called) in Rails is really just a fancy wrapper for the database. So, I created a second database connection, directly to the Sugar database!

You just have to setup new models and controllers in Rails. But, that&#8217;s not too hard. See this solution (http://pragdave.pragprog.com/pragdave/2006/01/sharing_externa.html). Use option 3. It worked well. Once you get the mapping figured out, you can even use the join tables, relationships, etc. It all works transparently.

I use this to synchronize various objects and fields.

Of course, you have to have access to the database. And, of course, I know I&#8217;m majorly in danger of screwing something up. And you have to figure out the inner workings of the Sugar database. And, of course, this might not work on the next version, etc., etc.

But, heck it is fast! And very easy to use!

If you want to know more, just let me know.
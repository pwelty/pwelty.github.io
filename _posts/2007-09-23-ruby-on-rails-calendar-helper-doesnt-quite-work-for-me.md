---
id: 6
title: 'Ruby on Rails Calendar Helper doesn&#8217;t quite work for me'
date: 2007-09-23T19:07:55-04:00
author: paul
layout: post
guid: http://www.paulwelty.com/ruby-on-rails/ruby-on-rails-calendar-helper-doesnt-quite-work-for-me/
permalink: /ruby-on-rails/ruby-on-rails-calendar-helper-doesnt-quite-work-for-me/
categories:
  - Ruby on Rails
---
[Geoffrey Grosenbach&#8217;s Ruby on Rails plugin calendar_helper](http://nubyonrails.com/) is simple and easy to use. Maybe I&#8217;m just picky, but one part of it just wasn&#8217;t working right for me.

Originally, it looks like this on line 96:

<pre style='overflow: scroll;'>cal &lt;&lt; %(&lt;caption class="#{options[:month_name_class]}"&gt;&lt;/caption&gt;&lt;thead&gt;&lt;tr&gt;&lt;th colspan="7"&gt;#{Date::MONTHNAMES[options[:month]]}&lt;/th&gt;&lt;/tr&gt;&lt;tr class="#{options[:day_name_class]}"&gt;)
</pre>

It doesn&#8217;t really make sense for the month name to be in a TH tag and the caption to be empty. So, I put the month name in the caption and eliminated the extra table row. In the end I changed it to this:

<pre style='overflow: scroll;'>cal &lt;&lt; %(&lt;caption class="#{options[:month_name_class]}"&gt;#{Date::MONTHNAMES[options[:month]]}&lt;/caption&gt;&lt;thead&gt;&lt;tr&gt;)
</pre>

This works well for me. If I knew anything about how to contribute to an open source project, I might propose a patch.
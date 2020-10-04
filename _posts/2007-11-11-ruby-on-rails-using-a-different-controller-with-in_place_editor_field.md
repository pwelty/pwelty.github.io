---
id: 9
title: 'Ruby on Rails: Using a different controller with in_place_editor_field'
date: 2007-11-11T08:30:35-04:00
author: paul
layout: post
guid: http://www.paulwelty.com/ruby-on-rails/ruby-on-rails-using-a-different-controller-with-in_place_editor_field/
permalink: /ruby-on-rails/ruby-on-rails-using-a-different-controller-with-in_place_editor_field/
categories:
  - Ruby on Rails
---
I don&#8217;t know why this took a while to figure out, but it did. If you are using the stock Rails in\_place\_editor_field, you know it looks like this in the controller:

<pre>in_place_edit_for :user, :name
</pre>

And like this in the view:

<pre>&lt;%= in_place_editor_field :user, :name %&gt;
</pre>

This works fine so long as you&#8217;re rendering from the users controller. But, what if this view is a partial inside a different controller&#8217;s view? In that case, what gets called is not &#8220;/users/set\_user\_name&#8221; but &#8220;/othercontroller/set\_user\_name&#8221;. And, of course, it fails because there is no method (dynamic or otherwise) like that there.

The solution is easy, but the documentation isn&#8217;t helpful. You need to alter the view to be like this:

<pre style='overflow: scroll;'>&lt;%= in_place_editor_field :user, :name, {}, :url=>{:controller=>'users', :action=>'set_user_name', :id=>user.id}} %&gt;
</pre>
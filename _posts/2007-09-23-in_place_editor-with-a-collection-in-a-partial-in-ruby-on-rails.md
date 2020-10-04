---
id: 4
title: In_place_editor with a collection in a partial in Ruby on Rails
date: 2007-09-23T14:40:13-04:00
author: paul
layout: post
guid: http://www.paulwelty.com/ruby-on-rails/in_place_editor-with-a-collection-in-a-partial-in-ruby-on-rails/
permalink: /ruby-on-rails/in_place_editor-with-a-collection-in-a-partial-in-ruby-on-rails/
categories:
  - Ruby on Rails
---
It seems like it would take a lot of work to get the in\_place\_editor to work in a partial on a collection, but it does. (It took me a lot of time to figure this out, but maybe I&#8217;m just more than average dense.) The best post to-date on this is at [we eat bricks](http://www.weeatbricks.com/2007/09/01/in_place_editor_field-method-in-ruby-on-rails/).

Just add the usual in the controller (user_controller.rb):

<pre>in_place_edit_for :user, :name
</pre>

And, of course, the method:

<pre>def edit
  @users = User.find(:all)
end
</pre>

Then, in the main view (edit.rhtml):

<pre>&lt;%= render :partial=>'user', :collection=>@users %>
</pre>

Then, in the partial (_users.rhtml):

<pre>&lt;%= in_place_editor_field :model, :column %&gt;
</pre>

At first, this won&#8217;t work. You will get an error that says &#8220;Called id for nil, which would mistakenly be 4 &#8212; if you really wanted the id of nil, use object\_id&#8221; on the line containing the &#8220;in\_place\_editor\_field&#8221;.

It turns out this is a bug, and there is a workaround. Just add this at the top of your partial:

<pre>&lt;%- @user = user -%&gt;
</pre>

I hope this helps someone save some time.
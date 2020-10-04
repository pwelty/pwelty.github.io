---
id: 5
title: Getting a remote form to submit within a partial collection when any select changes in Ruby on Rails
date: 2007-09-23T15:02:42-04:00
author: paul
layout: post
guid: http://www.paulwelty.com/ruby-on-rails/getting-a-remote-form-to-submit-within-a-partial-collection-when-any-select-changes-in-ruby-on-rails/
permalink: /ruby-on-rails/getting-a-remote-form-to-submit-within-a-partial-collection-when-any-select-changes-in-ruby-on-rails/
categories:
  - Ruby on Rails
---
This one is harder than it seems. But, I figured out a way. The trick and breakthrough came from [Teflon Ted](http://trak3r.blogspot.com/2006/04/in-place-select-and-submit-for-ruby-on.html).

With a regular form, you could do this in your select statement:

<pre>:onChange=>"this.form.submit();"
</pre>

This won&#8217;t work with a remote form, because the submission is not handled with the submit method but rather within the JavaScript callback in onsubmit. So, with a remote form, you have to change it to this:

<pre>:onChange=>"this.form.onsubmit();"
</pre>

So, here is my code.

<pre style="overflow: scroll;">&lt;%- remote_form_for
  :user,
  user,
  :url=>{:action=>'update_remote', :id=>user.id},
  :html=>{:id=>'form_'+user.id.to_s},
  :loading=>"Element.show('spinner_"+user.id.to_s+"'); Form.disable('form_"+user.id.to_s+"')"
  do |f|
-%&gt;

&lt;%= f.select
  :project_id,
  Project.find(:all).collect{|p| [p.name,p.id]},
  {:include_blank=>false, :selected=>user.project_id},
  {:onChange=>"this.form.onsubmit();", :id=>'user_project_id_'+user.id.to_s}
%&gt;

&lt;%- end -%&gt;



<div id="spinner_&lt;%= user.id.to_s %&gt;" style="display: none;" class='spinner'>
  &gt;%= image_tag 'spinner_arrows.gif' %&lt; Saving...
  
</div>
</pre>

Note that this is in a partial that gets iterated over a collection. So, I have to give everything a unique id in the HTML. Also, note that this includes the user of a spinner to show activity is taking place. I also like to disable the form temporarily to make sure nothing else gets selected. I don&#8217;t have to hide the spinner or reactivate the form because when the table row gets regenerated via RJS, it goes back to the default condition.
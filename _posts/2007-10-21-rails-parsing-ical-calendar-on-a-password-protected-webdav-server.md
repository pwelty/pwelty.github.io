---
id: 8
title: 'Rails: Parsing iCal calendar on a password-protected WebDAV server'
date: 2007-10-21T19:02:18-04:00
author: paul
layout: post
guid: http://www.paulwelty.com/ruby-on-rails/rails-parsing-ical-calendar-on-a-password-protected-webdav-server/
permalink: /ruby-on-rails/rails-parsing-ical-calendar-on-a-password-protected-webdav-server/
categories:
  - Ruby on Rails
---
It took me a little while, but I finally got this working. You&#8217;ll need the [iCalendar plugin](http://icalendar.rubyforge.org/).

<pre>require 'icalendar' 
def view_ical
    request = Net::HTTP::Get.new('/calendars/calendar.ics') 
   response = Net::HTTP.start('webdav.site.com') {|http| 
     request.basic_auth 'username', 'password' 
     response = http.request(request) 
   } 
   calendar_text = response.body
   calendars = Icalendar.parse(calendar_text) 
   calendar = calendars.first
end
</pre>
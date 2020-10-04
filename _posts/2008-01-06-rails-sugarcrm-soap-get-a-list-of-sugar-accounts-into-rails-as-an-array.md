---
id: 11
title: 'Rails + SugarCRM + SOAP &#8211; Get a list of Sugar accounts into Rails as an array'
date: 2008-01-06T10:05:12-04:00
author: paul
layout: post
guid: http://www.paulwelty.com/ruby-on-rails/rails-sugarcrm-soap-get-a-list-of-sugar-accounts-into-rails-as-an-array/
permalink: /ruby-on-rails/rails-sugarcrm-soap-get-a-list-of-sugar-accounts-into-rails-as-an-array/
categories:
  - Ruby on Rails
---
I have long wanted to make sure my CRM system (SugarCRM) and my project management system synchonized certain data, mainly company names. I hate having to sync stuff like that manually. So, I&#8217;ve been working on integrating the data using a SOAP client on the Rails side. It took all day to get this working. I don&#8217;t know why this took forever to find out, or why there aren&#8217;t many good references on the Web. (Maybe I&#8217;m just dense!)

I had to patch together a bunch of code, re-code some PHP examples, and do quite a bit of experimenting, to get this all working. Here is a list of some of the sites I used:

[http://www.sugarcrm.com/forums/showthread.php?t=17954&highlight=get\_entry\_list](http://www.sugarcrm.com/forums/showthread.php?t=17954&highlight=get_entry_list)
:   Good PHP examples about how certain SOAP calls are structured.

<http://www.ruby-doc.org/stdlib/libdoc/soap/rdoc/index.html>
:   Basics on how the SOAP objects work. Nothing really useful here, but it helped a little.

<http://www.beanizer.org/site/content/view/2/29/lang,en/>
:   Another good PHP reference.

<http://kousenit.wordpress.com/2006/08/08/ruby-web-service-clients/>
:   Has some general SOAP info, but not on SugarCRM

[http://www.sugarcrm.com/wiki/index.php?title=SOAP\_in\_RUBY](http://www.sugarcrm.com/wiki/index.php?title=SOAP_in_RUBY)
:   Sugar&#8217;s own starter directions. This is the backbone of the code below.

<http://www.sugarcrm.com/wiki/index.php?title=SOAP_Documentation>
:   Sugar&#8217;s SOAP documentation. I have to admit that this doesn&#8217;t make a lot of sense to me.

<http://martyhaught.com/articles/2006/08/04/mapping-soap-response-without-wsdl/>
:   Good example of how confusing this can be. Note that Marty&#8217;s situation is exactly where I got stuck. It turns out that these &#8220;special&#8221; attributes in the SOAP Mapping Object response (\_\_xmlattr, \_\_xmele, etc.) are not really important to the programmer. You can access the data with special attributes that refer to the attributes returned from the server. At least that&#8217;s my theory. So, in my example below, you access the results you want using the &#8220;result.entry\_list&#8221; attribute, because the &#8220;get\_entry_list&#8221; command returns that variable. Note that when you examine the results object, you don&#8217;t see these special attributes. I&#8217;m sure this is some special Ruby thing that I don&#8217;t understand.</ul> 

Anyway, here&#8217;s the code for getting a list of all companies, called &#8220;Accounts&#8221; in SugarCRM, into Rails in an array.

<pre style='overflow: scroll;'>def list_accounts
    require 'soap/wsdlDriver'
    require 'digest/md5'
    u = "username"
    p = Digest::MD5.hexdigest("password")
    ua = {"user_name" => u,"password" => p}
    wsdl = "http://your-sugar-web-site.com/soap.php?wsdl"

    #create soap
    s = SOAP::WSDLDriverFactory.new(wsdl).create_rpc_driver

    #uncomment this line for debugging. saves xml packets to files
    #s.wiredump_file_base = "soapresult"

    #create session
    ss = s.login(ua,nil)

    #check for login errors
    if ss.error.number.to_i != 0 

    	#status message
    	logger.debug "failed to login - #{ss.error.description}"

    	#exit program
    	exit

    else

    	#get id
    	sid = ss['id']

    	#get current user id
    	uid = s.get_user_id(sid)

    	#status message
    	logger.debug "logged in to session #{sid} as #{u} (#{uid})"

         #the part below is general. you can use it to get any type of data you want. just change the "module_name"

         module_name = "Accounts"

         query = "" # gets all the acounts, you can also use SQL like "accounts.name like '%company%'"
         order_by = "" # in default order. you can also use SQL like "accounts.name"
         offset = 0 # I guess this is like the SQL offset
         select_fields = ['name','industry'] # this can't be an empty array, my testing showed
         max_results = "1000000" # if set to 0 or "", this doesn't return all the results, like you'd expect
         deleted = 0 # whether you want to retrieve deleted records, too

         result = s.get_entry_list(sid,module_name,query,order_by,offset,select_fields,max_results,deleted)

         #below is where we build the array of names. note that everything gets returns in a name-value pairs hash (name_value_list), using the field list from the request

         @output = []
         for entry in result.entry_list
            item = {}
            for name_value in entry.name_value_list
              item[name_value.name]=name_value.value
            end
           @output &lt;&lt; item
         end
        
    	#logout
    	s.logout(sid)

    	#status message
    	logger.debug "logged out"
    	    	
    end
</pre>
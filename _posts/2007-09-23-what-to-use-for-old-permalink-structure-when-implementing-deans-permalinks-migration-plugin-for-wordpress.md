---
id: 3
title: 'What to use for old permalink structure when implementing Dean&#8217;s Permalinks Migration Plugin for WordPress'
date: 2007-09-23T13:13:26-04:00
author: paul
layout: post
guid: http://www.paulwelty.com/wordpress/what-to-use-for-old-permalink-structure-when-implementing-deans-permalinks-migration-plugin-for-wordpress/
permalink: /wordpress/what-to-use-for-old-permalink-structure-when-implementing-deans-permalinks-migration-plugin-for-wordpress/
categories:
  - Wordpress
---
If you want to move your WordPress permalinks via 301, you can try to do it by hand using rewrites in your .htaccess file. Much easier is [Dean&#8217;s Permalinks Migration Plugin for WordPress](http://www.deanlee.cn/?p=111).

On my work blog (<http://www.synaxisworks.com/blog/>), I used to use the default &#8220;?p=post-number&#8221; format, and I wanted to change to a more SEO-friendly format. I setup Dean&#8217;s plugin. The first problem is that I didn&#8217;t know what to put for the &#8220;old permalink structure&#8221;. I tried a million combinations of text, regex, and WordPress codes to try to get it to match the default format.

It turns out, according to this post, that the default permalinks never redirect and always work. So, the upshot is that I **can&#8217;t** redirect the default links and that I don&#8217;t really need Dean&#8217;s plugin at all. At least my new permalinks will be recorded in Google with the new format.
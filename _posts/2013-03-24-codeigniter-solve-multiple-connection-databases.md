---
id: 140
title: 'Codeigniter : Solve Multiple Connection databases'
date: 2013-03-24T12:32:51+00:00
author: justudin
layout: post
guid: http://justudin.wordpress.com/?p=140
permalink: /codeigniter-solve-multiple-connection-databases/
publicize_twitter_user:
  - udinjust4u
  - udinjust4u
tagazine-media:
  - 'a:7:{s:7:"primary";s:0:"";s:6:"images";a:0:{}s:6:"videos";a:0:{}s:11:"image_count";i:0;s:6:"author";s:8:"31399586";s:7:"blog_id";s:8:"32019069";s:9:"mod_stamp";s:19:"2013-03-24 12:32:51";}'
  - 'a:7:{s:7:"primary";s:0:"";s:6:"images";a:0:{}s:6:"videos";a:0:{}s:11:"image_count";i:0;s:6:"author";s:8:"31399586";s:7:"blog_id";s:8:"32019069";s:9:"mod_stamp";s:19:"2013-03-24 12:32:51";}'
categories:
  - Web Programming
tags:
  - ci
  - ci 2.0
  - connection
  - database
  - multiple
  - oracle
  - php
  - Web Programming
---
Hello there, i&#8217;m here just wanna share my problem. Here i have a problem when i call my database connection on my model. <span style="line-height: 1.714285714; font-size: 1rem;">But i was finally solve it with myself :D. So i just wanna share you, so if you have the same problem you can follow this trick.</span>
  
Here my 2 database config name.<!--more-->

<pre>$db['sia']['hostname'] = "localhost";
$db['sialumni']['hostname'] = "localhost";</pre>

when i wanna use &#8220;**sia**&#8221; database on my model with this line of code :

<pre>$this-&gt;load-&gt;database('sia', TRUE);
$q=$this-&gt;db-&gt;get('table');
return $q;</pre>

but i got an error. so i solve it with this line of code :

<pre>$this-&gt;db_sia=$this-&gt;load-&gt;database('sia', TRUE);
$q=$this-&gt;db_sia-&gt;get('table');
return $q;</pre>

So all is good as well as i fixed it.
  
Thank you for visiting and reading my notes. I hope its usefull for me and you.

See you next time, bye bye <img src="http://test.justudin.com/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

Kindly Regards,
  
justudin
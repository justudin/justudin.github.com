---
id: 140
title: 'Codeigniter : Solve Multiple Connection databases'
date: 2013-03-24T12:32:51+00:00
author: justudin
layout: post
guid: http://justudin.wordpress.com/?p=140
permalink: /codeigniter-solve-multiple-connection-databases/
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
Hello there, i’m here just wanna share my problem. Here i have a problem when i call my database connection on my model. *But i was finally solve it with myself :D. So i just wanna share you, so if you have the same problem you can follow this trick.*

Here my 2 database config name.

```bash
$db'sia' = "localhost";
$db'sialumni' = "localhost";
```

when i wanna use “**sia**” database on my model with this line of code :

```bash
$this->load->database('sia', TRUE);
q=this->db->get('table');
return $q;
```

but I got an error. so i solved it with this line of code :

```bash
$this->db_sia=this->load->database('sia', TRUE);
q=this->db_sia->get('table');
return $q;
```

So all is good as well as I **fixed** it.

Thank you for visiting and reading my notes. 

I hope its usefull for me and you.

See you next time, bye bye :)
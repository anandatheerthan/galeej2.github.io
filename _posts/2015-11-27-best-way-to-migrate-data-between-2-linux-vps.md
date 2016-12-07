---
layout: post
title: Best Way to Migrate Data between 2 Linux VPS
date: 2015-11-27 02:59
author: administrator
comments: true
categories: [Linux]
---
If you have root access, you can ftp (or sftp) from one server directly to the other. Or you could log into server1 and run rsync from cmd line like this:
<pre class="lang:default decode:true ">rsync -av /var/www/html root@192.168.0.100:/var/www/html</pre>
&nbsp;

replace '/var/www/html' with your folder path and replace '192.168.0.100' with your server2 ip address

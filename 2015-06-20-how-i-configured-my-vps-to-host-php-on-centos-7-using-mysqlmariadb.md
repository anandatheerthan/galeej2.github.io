---
layout: post
title: How I configured my VPS to host PHP on CentOS 7 using MySQL(MariaDB)
date: 2015-06-20 01:49
author: administrator
comments: true
categories: [Reference]
---
I purchased VPS from CrownCloud and wanted to setup to host php applications. This is what I did to setup and host a sample php page.

1) Login as root using SSH
2) verify httpd is already using "which httpd"
3) install php using yum install php(Note, files should be placed under /var/www/html)
4) open port 80 and add to firewall else you will not be able to access your page from internet
iptables -I INPUT 5 -p tcp -m tcp --dport 80 -j ACCEPT
service itables save
service iptables restart
service httpd restart
5) To verify whether port 80 is open, use nmap to check the results.
6) Install mysql, yum install mariadb-server (latest change that mysql renamed to mariadb)
and secure the DB using /usr/bin/mysql_secure_installation.If you want mysql to be accessed from outside,
add the rules to iptables
-I INPUT -p tcp --dport 3306 -m state --state NEW,ESTABLISHED -j ACCEPT
-I OUTPUT -p tcp --sport 3306 -m state --state ESTABLISHED -j ACCEPT
service iptables save
service iptables restart
service mariadb restart
7) Install ftp client and configure users using
https://ostechnix.wordpress.com/2013/12/15/setup-ftp-server-step-by-step-in-centos-6-x-rhel-6-x-scientific-linux-6-x/

http://www.rackspace.com/knowledge_center/article/rackspace-cloud-essentials-centos-installing-vsftpd
<pre class="default prettyprint prettyprinted"><code><span class="pln">iptables </span><span class="pun">-</span><span class="pln">D INPUT </span><span class="pun">{</span><span class="pln">line</span><span class="pun">}</span></code></pre>
<pre id="pre-11" class="p1">sudo iptables -I INPUT 4 -m tcp -p tcp -m conntrack --ctstate NEW --dport 21 -j ACCEPT</pre>
<pre class="default prettyprint prettyprinted"></pre>
8) Install phpmyadmin using
https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-with-apache-on-a-centos-7-server

Change the below to access from internet
Options Indexes FollowSymLinks MultiViews
AllowOverride all
Require all granted

---
layout: post
title: Multi Source Replication - MariaDB
date: 2015-11-28 07:40
author: administrator
comments: true
categories: [MySql]
---
As with version 10.0.1, it is now possible to use multiple masters as source for single slave node as replication topology.

<a href="https://mariadb.com/kb/en/mariadb/documentation/replication/standard-replication/setting-up-replication/">This</a> link can help you set up the replication from a single master. To add more masters just use the 'CHANGE MASTER TO' command and use different master addresses.

Update: Follow <a href="https://www.digitalocean.com/community/tutorials/how-to-set-up-master-slave-replication-in-mysql" target="_blank">this</a> to setup basic replication.

Example

To add two masters, use
<pre class="lang:mysql decode:true ">CHANGE MASTER "source_1" TO 
  MASTER_HOST='XXX.XXX.XXX.XX1',
  MASTER_USER='replication_user',
  MASTER_LOG_FILE='mysql-bin.000001',
  MASTER_LOG_POS=564;

CHANGE MASTER "source_2" TO 
  MASTER_HOST='XXX.XXX.XXX.XX2',
  MASTER_USER='slave_user',
  MASTER_PASSWORD='password',
   MASTER_LOG_FILE='mysql-bin.000002',
  MASTER_LOG_POS=107;

START ALL SLAVES;</pre>
&nbsp;

This should create a multi-source instance in MariaDB which will consolidate data from all your sources.

To view all your sources, run the <code>SHOW ALL SLAVES STATUS</code> \G command from your slave MariaDB instance.

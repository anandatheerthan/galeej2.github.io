---
layout: post
title: MariaDB Event Scheduler
date: 2015-12-22 00:01
author: administrator
comments: true
categories: [MySql]
---
<b>Enable MySQL Event Scheduler</b>
Start MySQL event scheduler by executing following query in PhpMyAdmin or MySQL command prompt.
<div class="code">
<pre class="lang:mysql decode:true ">SET GLOBAL event_scheduler = ON;
Or
SET GLOBAL event_scheduler = 1;</pre>
<b>Create a Event</b>
Here the following event will run everyday and clear/delete 10 days old data from<i>cart</i> table based on time stamp
<div class="code">
<pre class="lang:mysql decode:true ">CREATE EVENT newEvent
ON SCHEDULE EVERY 1 DAY
DO
DELETE FROM cart WHERE created_at &lt;= DATE_SUB(NOW(), INTERVAL 10 DAY) ;</pre>
<b>View Event</b>
Show all the running events.
<div class="code">
<pre class="lang:mysql decode:true ">SHOW EVENTS;</pre>
&nbsp;

</div>
</div>
</div>

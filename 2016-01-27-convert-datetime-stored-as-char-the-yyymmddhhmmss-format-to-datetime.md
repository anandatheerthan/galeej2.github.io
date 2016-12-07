---
layout: post
title: Convert datetime stored as char the YYYMMDDHHmmSS format to datetime
date: 2016-01-27 15:02
author: administrator
comments: true
categories: [SQL]
---
<pre class="lang:mysql decode:true ">declare @S varchar(50)
set @S = '20120606122012'

select cast(left(@S, 8)+' '+substring(@S, 9, 2)+':'+substring(@S, 11, 2)+':'+substring(@S, 13, 2) as datetime)</pre>
&nbsp;

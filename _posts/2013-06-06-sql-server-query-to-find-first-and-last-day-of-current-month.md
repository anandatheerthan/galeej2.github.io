---
layout: post
title: SQL SERVER – Query to Find First and Last Day of Current Month
date: 2013-06-06 00:18
author: administrator
comments: true
categories: [SQL]
---
Following query will run respective to today’s date. It will return Last Day of Previous Month, First Day of Current Month, Today, Last Day of Previous Month and First Day of Next Month respective to current month.<br/><br/><code>DECLARE @mydate DATETIME<br/>SELECT @mydate = GETDATE()<br/>SELECT CONVERT(VARCHAR(25),DATEADD(dd,-(DAY(@mydate)),@mydate),101) ,<br/>'Last Day of Previous Month'<br/>UNION<br/>SELECT CONVERT(VARCHAR(25),DATEADD(dd,-(DAY(@mydate)-1),@mydate),101) AS Date_Value,<br/>'First Day of Current Month' AS Date_Type<br/>UNION<br/>SELECT CONVERT(VARCHAR(25),@mydate,101) AS Date_Value, 'Today' ASDate_Type<br/>UNION<br/>SELECT CONVERT(VARCHAR(25),DATEADD(dd,-(DAY(DATEADD(mm,1,@mydate))),DATEADD(mm,1,@mydate)),101) ,<br/>'Last Day of Current Month'<br/>UNION<br/>SELECT CONVERT(VARCHAR(25),DATEADD(dd,-(DAY(DATEADD(mm,1,@mydate))-1),DATEADD(mm,1,@mydate)),101) ,<br/>'First Day of Next Month'<br/>GO</code><br/>Reference : <strong>Pinal Dave (</strong><a href="http://blog.sqlauthority.com/" target="_blank"><strong>http://blog.SQLAuthority.com</strong></a><strong>)</strong>

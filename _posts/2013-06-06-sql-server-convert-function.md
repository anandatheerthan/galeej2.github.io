---
layout: post
title: SQL Server CONVERT() Function
date: 2013-06-06 01:15
author: administrator
comments: true
categories: [SQL]
---
<h3>The following script uses the CONVERT() function to display different formats. We will use the GETDATE() function to get the current date/time:</h3><br/><div><br/><div>CONVERT(VARCHAR(19),GETDATE())<br/>CONVERT(VARCHAR(10),GETDATE(),10)<br/>CONVERT(VARCHAR(10),GETDATE(),110)<br/>CONVERT(VARCHAR(11),GETDATE(),6)<br/>CONVERT(VARCHAR(11),GETDATE(),106)<br/>CONVERT(VARCHAR(24),GETDATE(),113)</div><br/></div><br/>The result would look something like this:<br/><div><br/><div>Nov 04 2011 11:45 PM<br/>11-04-11<br/>11-04-2011<br/>04 Nov 11<br/>04 Nov 2011<br/>04 Nov 2011 11:45:34:243</div><br/></div>

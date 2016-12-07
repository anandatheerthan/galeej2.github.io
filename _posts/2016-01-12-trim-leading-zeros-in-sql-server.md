---
layout: post
title: Trim Leading Zeros in SQL Server
date: 2016-01-12 10:19
author: administrator
comments: true
categories: [SQL Server]
---
You this expression in queries to trim leading zeros. Replace col with your column name.
<pre class="lang:plsql decode:true ">SUBSTRING(col, PATINDEX('%[^0]%', col+'.'), LEN(col))</pre>
&nbsp;

---
layout: post
title: Catch Integrity Violation in laravel
date: 2016-05-13 18:30
author: administrator
comments: true
categories: [Laravel]
---
If you have defined unique index on your MySQL tables, insertion can fail if you try to insert duplicate records. You can actually catch such scenarios and handle according to the requirement.
<pre class="lang:default decode:true ">try
{
// do DB insert
}
catch(\Illuminate\Database\QueryException $e)
{
$errorCode = $e-&gt;errorInfo[1];
if($errorCode == 1062){
// houston, we have a duplicate entry problem
}</pre>
&nbsp;

---
layout: post
title: SQL - `IN` operator with combination of columns
date: 2016-01-28 01:48
author: administrator
comments: true
categories: [SQL]
---
If you write SQL queries often, you should have probably used the <code>IN</code> operator which determines if a specified value matches any value in a list or a subquery. Below is the most simple use-case with single value, for examle:
<pre class="lang:plsql decode:true ">SELECT	* 
FROM 	`students`
WHERE 	id NOT IN (1,5,6,3)</pre>
&nbsp;

But one thing that you might not know is that you can use that for a combination of values as well. For example lets take a table where there are student names and subjects

<img src="http://i.imgur.com/q7VZHxk.png" alt="Students Table" />

And there are some user and subject combinations that we do not want, lets say below are the ones that we do not want:

<img src="http://i.imgur.com/L0dK0DR.png" alt="Not Required Columns" />

In that case, our SQL would look like the following:
<pre class="lang:mysql decode:true ">SELECT * 
FROM   students 
WHERE 
	( name, subject )
NOT IN 
	(
		('Jane Doe', 'Analysis of Algorithms'),
		('John Doe', 'Software Engineering - II'),
		('Jane Doe', 'Professional Practices')
	);</pre>
&nbsp;

The list used in <code>NOT IN</code> might be provided in the form of list i.e. the way it is provided in the above example or it might be returned from some subquery.

---
layout: post
title: MySQL Compress Backup
date: 2015-12-03 03:33
author: administrator
comments: true
categories: [MySql]
---
<ul>
<ul>
<ul>
<ul style="text-align: left;">There are several strategies for backup, snapshot, dump, dump binlog, it all depends on your need and the size of your database. I’ll explain a little about the tool provides by MySQL, which is the</ul>
</ul>
</ul>
</ul>
<span style="font-family: monospace, serif; font-size: 15px; line-height: 1.6;">mysqldump</span>
<ul>
<ul>
<ul style="text-align: left;">, I indicate this tool for databases that have 15gb/20gb even more than that, the probability that you have problems to restore a backup and long delay, make it unfeasible.How mysqldump works? He does nothing but create sql commands to our structure and data and put them in the file specified.First, I will explain some of the most important options mysqldump then, for those who have MySQL installed on a Linux server, I will teach how to compress the dump in real-time.</ul>
</ul>
</ul>
<strong>all databases</strong>
<pre class="lang:mysql decode:true ">mysqldump -u usuario -p --all-databases &gt; dump.sql</pre>
<strong>one database</strong>
<pre class="lang:mysql decode:true ">mysqldump -u usuario -p --databases db1 &gt; dump.sql</pre>
<strong>many databases</strong>
<pre class="lang:mysql decode:true ">mysqldump -u usuario -p --databases db1 db2 db... &gt; dump.sql</pre>
<strong>triggers</strong>
<pre class="lang:mysql decode:true ">mysqldump -u usario -p --triggers --all-databases &gt; dump.sql</pre>
<strong>procedures and functions</strong>
<ul>
<ul>:</ul>
</ul>
&nbsp;
<pre class="lang:mysql decode:true ">mysqldump -u usuario -p --routines --all-databases &gt; dump.sql</pre>
<ul>Now let’s compress our dump in real time with</ul>
<strong>gzip</strong>:
<pre class="lang:mysql decode:true ">mysqldump -u usuario -p --all-databases | gzip &gt; dump.sql.gz</pre>
<ul>We can still reach a higher compression ratio using the</ul>
<strong>bzip2</strong>:
<pre class="lang:mysql decode:true ">mysqldump -u usuario -p --all-databases | bzip2 &gt; dump.sql.bz2</pre>
And how do I restore the dump?

<strong>Normal</strong>:
<pre class="lang:mysql decode:true ">mysql -u usuario -p &lt; dump.sql</pre>
<strong>gzip</strong>:
<pre class="lang:mysql decode:true ">gunzip &lt; dump.sql.gz | mysql -u usuario -p</pre>
<strong>bzip2</strong>:
<pre class="lang:mysql decode:true ">bunzip2 &lt; dump.sql.bz2 | mysql -u usuario -p</pre>
&nbsp;

---
layout: post
title: How to check if your site is using HHVM
date: 2015-10-24 10:35
author: administrator
comments: true
categories: [Linux, PHP]
---
If you have configured HHVM to work with nginx or apache and wondered how to check if your site is actually using HHVM to render the site? You can check using curl commands,
<pre class="lang:default decode:true ">curl -I example.com</pre>
you should be seeing something like below in your output,
<pre class="lang:default decode:true ">X-Powered-By: HHVM/3.2.0</pre>
&nbsp;

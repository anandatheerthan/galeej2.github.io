---
layout: post
title: Eloquent collection: counting and detect empty
date: 2015-09-11 03:40
author: administrator
comments: true
categories: [Laravel]
---
To determine if laravel collection is empty
<pre class="lang:default decode:true default prettyprint prettyprinted ">if ($result-&gt;first()) { } 
if (!$result-&gt;isEmpty()) { }
if ($result-&gt;count()) { }</pre>

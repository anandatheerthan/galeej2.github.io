---
layout: post
title: Is your php code not getting executed
date: 2015-06-20 11:14
author: administrator
comments: true
categories: [Reference]
---
If your PHP code is not getting executed and see the actual php code in your browser, there might be chances that apache is not set to handle php files.

If you have installed <code>php</code>, then make sure that it is loaded by <code>apache</code> and <code>apache</code> is associated with<code>php</code> handler.
<pre><code>LoadModule php5_module        modules/libphp5.so
AddType application/x-httpd-php .php
</code></pre>
And you should check your <code>.htaccess</code>. It may have some configurations that overrided apache's config.

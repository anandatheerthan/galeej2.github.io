---
layout: post
title: Redirect HTTP traffic to HTTPS
date: 2015-09-11 03:28
author: administrator
comments: true
categories: [PHP]
---
here is how you redirect all traffic to https if you have installed an SSL certificate.
<pre><code>RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI} [R,L]</code></pre>

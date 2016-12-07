---
layout: post
title: Fix Jetpack XML RPC error
date: 2016-01-20 01:22
author: administrator
comments: true
categories: [Wordpress]
---
If you have an SSL enabled WordPress site with Jetpack installed, you might face issues while connecting to WordPress.com. Below steps can help although there might be various reasons. This one solved my issue though.
<ol>
	<li>Goto Settings and make site address and wordpress address to use HTTPS</li>
	<li>add <code class="php plain">define(</code><code class="php string">'FORCE_SSL_ADMIN'</code><code class="php plain">, true); in wp-config.php</code></li>
	<li>add <code class="php variable">$_SERVER</code><code class="php plain">[</code><code class="php string">'SERVER_PORT'</code><code class="php plain">] = 443; in wp-config.php</code></li>
	<li>Deactivate and reactivate Jetpack.</li>
</ol>

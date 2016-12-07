---
layout: post
title: Easily change old blog url - Wordpress
date: 2016-05-10 16:00
author: administrator
comments: true
categories: [Wordpress]
---
To update WordPress options with the new blog location, use the following SQL command:
<pre class="lang:default decode:true ">UPDATE wp_options SET option_value = replace(option_value, 'http://www.old-domain.com', 'http://www.new-domain.com') WHERE option_name = 'home' OR option_name = 'siteurl';</pre>
After that  fix URLs of the WordPress posts and pages stored in database wp_posts table
<pre class="lang:default decode:true ">UPDATE wp_posts SET guid = replace(guid, 'http://www.old-domain.com','http://www.new-domain.com');</pre>
Use the following SQL commands to fix all internal links
<pre class="lang:default decode:true ">UPDATE wp_posts SET post_content = replace(post_content, 'http://www.old-domain.com', 'http://www.new-domain.com');</pre>
&nbsp;

---
layout: post
title: Avoiding the burden of file uploads
date: 2016-06-29 06:02
author: administrator
comments: true
categories: [Laravel]
---
Handling file uploads sucks. Code-wise it's a fairly simple task, the files get sent along with a POST request and are available server-side in the <code>$_FILES</code> super global. Your framework of choice may even have a convenient way of dealing with these files, probably based on Symfony's <a href="http://api.symfony.com/2.3/Symfony/Component/HttpFoundation/File/UploadedFile.html">UploadedFile</a> class. Unfortunately it's not that simple. You'll also have to change some PHP configuration values like <code>post_max_size</code> and <code>upload_max_filesize</code>, which complicates your infrastructure provisioning and deployments. Handling large file uploads also causes high disk I/O and bandwidth use, forcing your web servers to work harder and potentially costing you more money.

<a href="https://cwhite.me/avoiding-the-burden-of-file-uploads/">More</a>

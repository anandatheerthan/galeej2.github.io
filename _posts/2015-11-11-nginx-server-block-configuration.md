---
layout: post
title: Nginx Server Block Configuration
date: 2015-11-11 02:15
author: administrator
comments: true
categories: [Nginx]
---
The server block configuration for Nginx needs to be changed depending on whether the application is built on Laravel or wordpress or core PHP. Below configs can be used based on the type of PHP application you are deploying.

Laravel
<div>
<pre class="lang:default decode:true ">location / {                                                                                                                                           
                # First attempt to serve request as file, then                                                                                                 
                # as directory, then fall back to displaying a 404.                                                                                            
                #try_files $uri $uri/ =404;                                                                                                                    
                try_files $uri $uri/ /index.php$is_args$args;                                                                                                  
                # Uncomment to enable naxsi on this location                                                                                                   
                # include /etc/nginx/naxsi.rules                                                                                                               
        }</pre>
Wordpress
<pre class="lang:default decode:true ">location / {                                                                                                                                           
                # First attempt to serve request as file, then                                                                                                 
                # as directory, then fall back to displaying a 404.                                                                                            
                #try_files $uri $uri/ =404;                                                                                                                    
                try_files $uri $uri/ /index.php?$args;                                                                                                         
                # Uncomment to enable naxsi on this location                                                                                                   
                # include /etc/nginx/naxsi.rules                                                                                                               
        }</pre>
Core PHP
<pre class="lang:default decode:true "> location / {                                                                                                                                           
                # First attempt to serve request as file, then                                                                                                 
                # as directory, then fall back to displaying a 404.                                                                                            
                try_files $uri $uri/ =404;                                                                                                                     
                # Uncomment to enable naxsi on this location                                                                                                   
                # include /etc/nginx/naxsi.rules                                                                                                               
        }</pre>
&nbsp;

<span style="line-height: 1.5;">     </span></div>

---
layout: post
title: HHVM, Nginx and Ubuntu
date: 2015-11-11 00:49
author: administrator
comments: true
categories: [Linux, PHP]
---
HHVM is an <a href="http://github.com/facebook/hhvm">open-source</a> virtual machine designed for executing programs written in <a href="http://hacklang.org/">Hack</a>and <a href="http://php.net/">PHP</a>. HHVM uses a just-in-time (JIT) compilation approach to achieve superior performance while maintaining the development flexibility that PHP provides.

HHVM runs much of the world’s <a href="http://hhvm.com/frameworks">existing PHP</a>. <a href="http://hhvm.h4cc.de/">Developers</a> and <a href="http://www.hhvm.com/blog/1379/hhvm-on-heroku">hosts</a> are adopting HHVM.Rather than directly interpret or <a href="https://en.wikipedia.org/wiki/HipHop_for_PHP#History_Before_HHVM">compile PHP code directly to C++</a>, HHVM compiles Hack and PHP into an intermediate bytecode. This bytecode is then translated into <a title="X64" href="https://en.wikipedia.org/wiki/X64">x64</a> machine code dynamically at runtime by a just-in-time (<a title="Just-in-time compilation" href="https://en.wikipedia.org/wiki/Just-in-time_compilation">JIT</a>) compiler. This compilation process allows for all sorts of optimizations that cannot be made in a statically compiled binary, thus enabling higher performance of your Hack and PHP programs.

If you already have Nginx and php-fpm running you could easily install hhvm and repoint so that all php pages are executed on hhvm delivering faster content.

Below are the steps to install and configure hhvm to work with nginx.
<ol>
	<li>apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0x5a16e7281be7a449</li>
	<li>add-apt-repository "deb http://dl.hhvm.com/ubuntu $(lsb_release -sc) main"</li>
	<li>apt-get update</li>
	<li>apt-get install hhvm</li>
	<li>update-rc.d hhvm defaults</li>
	<li>/usr/share/hhvm/install_fastcgi.sh</li>
	<li>vi /etc/hhvm/server.ini</li>
	<li>remove line hhvm.server.port</li>
	<li>add below
<pre class="code-pre "><code langs="">hhvm.server.file_socket=/var/run/hhvm/hhvm.sock</code></pre>
</li>
	<li>service hhvm restart</li>
	<li>vi /etc/nginx/hhvm.conf</li>
	<li>make sure fastcgi line looks like below
<pre class="code-pre "><code langs="">fastcgi_pass <span class="highlight">unix:/var/run/hhvm/hhvm.sock</span>;</code>
</pre>
</li>
	<li>service nginx restart</li>
	<li>Run php --version and check the output, it should return HHVM.</li>
	<li>Now make separate config file in /etc/nginx/sites-available and symlink to /etc/nginx/sites-enabled to make your site up and running.</li>
	<li>Remember to comment out lines as shown below and include hhvm.conf in your virtual host files.<a href="http://www.rsa1.xyz/wp-content/uploads/2015/11/Capture.png"><img class="alignnone size-medium wp-image-425" src="http://www.rsa1.xyz/wp-content/uploads/2015/11/Capture-300x228.png" alt="NGinx config" width="300" height="228" /></a></li>
</ol>

---
layout: post
title: Secure VPS by changing SSH port
date: 2015-11-27 07:03
author: administrator
comments: true
categories: [Linux]
---
<h4>To Change the SSH Port for Your Linux Server</h4>
<ol>
	<li>Connect to your server via SSH .</li>
	<li>Switch to the root user .</li>
	<li>Run the following command:
<div class="hacker">vi /etc/ssh/sshd_config</div></li>
	<li>Locate the following line:
<div class="hacker"># Port 22</div></li>
	<li>Remove <strong>#</strong> and change <strong>22</strong> to your desired port number.</li>
	<li>Restart the <strong>ssh</strong> service by running the following command:
<div class="hacker">
<pre class="lang:default decode:true ">service ssh restart</pre>
&nbsp;

</div></li>
</ol>

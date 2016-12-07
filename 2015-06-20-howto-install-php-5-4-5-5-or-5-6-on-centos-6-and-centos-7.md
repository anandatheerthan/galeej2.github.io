---
layout: post
title: Howto Install PHP 5.4, 5.5 or 5.6 on CentOS 6 and CentOS 7
date: 2015-06-20 10:27
author: administrator
comments: true
categories: [Reference]
---
<h2>Repo Installation</h2>
Open up a SSH connection to your server and run the following commands (make sure you run as sudo if you need to):
<h3>For CentOS 7 (including EPEL install)</h3>
<div>
<div id="highlighter_76474" class="syntaxhighlighter  bash  ">
<table border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td class="gutter">
<div class="line number1 index0 alt2">1</div>
<div class="line number2 index1 alt1">2</div>
<div class="line number3 index2 alt2">3</div></td>
<td class="code">
<div class="container">
<div class="line number1 index0 alt2"><code class="bash plain">wget http:</code><code class="bash plain">//dl</code><code class="bash plain">.fedoraproject.org</code><code class="bash plain">/pub/epel/7/x86_64/e/epel-release-7-5</code><code class="bash plain">.noarch.rpm</code></div>
<div class="line number2 index1 alt1"><code class="bash plain">wget http:</code><code class="bash plain">//rpms</code><code class="bash plain">.famillecollet.com</code><code class="bash plain">/enterprise/remi-release-7</code><code class="bash plain">.rpm</code></div>
<div class="line number3 index2 alt2"><code class="bash plain">rpm -Uvh remi-release-7*.rpm epel-release-7*.rpm</code></div>
</div></td>
</tr>
</tbody>
</table>
</div>
</div>
If you already have EPEL installed:
<div>
<div id="highlighter_628827" class="syntaxhighlighter  plain">
<table border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td class="gutter">
<div class="line number1 index0 alt2">1</div>
<div class="line number2 index1 alt1">2</div></td>
<td class="code">
<div class="container">
<div class="line number1 index0 alt2"><code class="plain plain">wget <a href="http://rpms.famillecollet.com/enterprise/remi-release-7.rpm">http://rpms.famillecollet.com/enterprise/remi-release-7.rpm</a></code></div>
<div class="line number2 index1 alt1"><code class="plain plain">rpm -Uvh remi-release-7*.rpm</code></div>
</div></td>
</tr>
</tbody>
</table>
</div>
</div>
<h3>For CentOS 6 (including EPEL install)</h3>
<div>
<div id="highlighter_550020" class="syntaxhighlighter  plain">
<table border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td class="gutter">
<div class="line number1 index0 alt2">1</div>
<div class="line number2 index1 alt1">2</div>
<div class="line number3 index2 alt2">3</div></td>
<td class="code">
<div class="container">
<div class="line number1 index0 alt2"><code class="plain plain">wget <a href="http://dl.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm">http://dl.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm</a></code></div>
<div class="line number2 index1 alt1"><code class="plain plain">wget <a href="http://rpms.famillecollet.com/enterprise/remi-release-6.rpm">http://rpms.famillecollet.com/enterprise/remi-release-6.rpm</a></code></div>
<div class="line number3 index2 alt2"><code class="plain plain">rpm -Uvh remi-release-6*.rpm epel-release-6*.rpm</code></div>
</div></td>
</tr>
</tbody>
</table>
</div>
</div>
If you already have EPEL installed:
<div>
<div id="highlighter_3134" class="syntaxhighlighter  plain">
<table border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td class="gutter">
<div class="line number1 index0 alt2">1</div>
<div class="line number2 index1 alt1">2</div></td>
<td class="code">
<div class="container">
<div class="line number1 index0 alt2"><code class="plain plain">wget <a href="http://rpms.famillecollet.com/enterprise/remi-release-6.rpm">http://rpms.famillecollet.com/enterprise/remi-release-6.rpm</a></code></div>
<div class="line number2 index1 alt1"><code class="plain plain">rpm -Uvh remi-release-6*.rpm</code></div>
</div></td>
</tr>
</tbody>
</table>
</div>
</div>
<h2>Enabling the Repo</h2>
Now we need to make sure the repo is enabled and select which version you want to install. We need to head over to<code>/etc/yum.repos.d</code> you should inside see a file called <code>remi.repo</code>.

Open the file in your favourite editor (Nano, Pico, Vi etc), you’ll see a number of sections. We need to make sure that the first section <code>[remi]</code> is enabled:
<div>
<div id="highlighter_550102" class="syntaxhighlighter  plain">
<table border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td class="gutter">
<div class="line number1 index0 alt2">1</div>
<div class="line number2 index1 alt1">2</div>
<div class="line number3 index2 alt2">3</div>
<div class="line number4 index3 alt1">4</div>
<div class="line number5 index4 alt2">5</div>
<div class="line number6 index5 alt1">6</div>
<div class="line number7 index6 alt2">7</div></td>
<td class="code">
<div class="container">
<div class="line number1 index0 alt2"><code class="plain plain">[remi]</code></div>
<div class="line number2 index1 alt1"><code class="plain plain">name=Les RPM de remi pour Enterprise Linux 6 - $basearch</code></div>
<div class="line number3 index2 alt2"><code class="plain plain">#baseurl=<a href="http://rpms.famillecollet.com/enterprise/6/remi/">http://rpms.famillecollet.com/enterprise/6/remi/</a>$basearch/</code></div>
<div class="line number4 index3 alt1"><code class="plain plain">mirrorlist=<a href="http://rpms.famillecollet.com/enterprise/6/remi/mirror">http://rpms.famillecollet.com/enterprise/6/remi/mirror</a></code></div>
<div class="line number5 index4 alt2"><code class="plain plain">enabled=1</code></div>
<div class="line number6 index5 alt1"><code class="plain plain">gpgcheck=1</code></div>
<div class="line number7 index6 alt2"><code class="plain plain">gpgkey=<a href="file:///etc/pki/rpm-gpg/RPM-GPG-KEY-remi">file:///etc/pki/rpm-gpg/RPM-GPG-KEY-remi</a></code></div>
</div></td>
</tr>
</tbody>
</table>
</div>
</div>
Note the line <code>enabled=1</code> make sure this is set! Now technically you can actually go ahead and install PHP, but you will only get PHP 5.4.*. Which might be want to you want is so skip ahead to the next section!

If we want PHP 5.5 or PHP 5.6 we need to do a bit more work, further down in the <code>repo.repo</code> file you will see two additional sections <code>[remi-php55]</code> and <code>[remi-php56]</code>, decide which PHP version you want to install and then enable the correct. So for PHP 5.6 we would change to:
<div>
<div id="highlighter_206580" class="syntaxhighlighter  plain">
<table border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td class="gutter">
<div class="line number1 index0 alt2">1</div>
<div class="line number2 index1 alt1">2</div>
<div class="line number3 index2 alt2">3</div>
<div class="line number4 index3 alt1">4</div>
<div class="line number5 index4 alt2">5</div>
<div class="line number6 index5 alt1">6</div>
<div class="line number7 index6 alt2">7</div>
<div class="line number8 index7 alt1">8</div></td>
<td class="code">
<div class="container">
<div class="line number1 index0 alt2"><code class="plain plain">[remi-php56]</code></div>
<div class="line number2 index1 alt1"><code class="plain plain">name=Les RPM de remi de PHP 5.6 pour Enterprise Linux 6 - $basearch</code></div>
<div class="line number3 index2 alt2"><code class="plain plain">#baseurl=<a href="http://rpms.famillecollet.com/enterprise/6/php56/">http://rpms.famillecollet.com/enterprise/6/php56/</a>$basearch/</code></div>
<div class="line number4 index3 alt1"><code class="plain plain">mirrorlist=<a href="http://rpms.famillecollet.com/enterprise/6/php56/mirror">http://rpms.famillecollet.com/enterprise/6/php56/mirror</a></code></div>
<div class="line number5 index4 alt2"><code class="plain plain"># WARNING: If you enable this repository, you must also enable "remi"</code></div>
<div class="line number6 index5 alt1"><code class="plain plain">enabled=1</code></div>
<div class="line number7 index6 alt2"><code class="plain plain">gpgcheck=1</code></div>
<div class="line number8 index7 alt1"><code class="plain plain">gpgkey=<a href="file:///etc/pki/rpm-gpg/RPM-GPG-KEY-remi">file:///etc/pki/rpm-gpg/RPM-GPG-KEY-remi</a></code></div>
</div></td>
</tr>
</tbody>
</table>
</div>
</div>
Once you made your changes save your modified file and quit your editor.
<h2>Installing PHP</h2>
Now I’m assuming you don’t already have PHP installed, this bit is super simple.
<div>
<div id="highlighter_671310" class="syntaxhighlighter  plain">
<table border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td class="gutter">
<div class="line number1 index0 alt2">1</div></td>
<td class="code">
<div class="container">
<div class="line number1 index0 alt2"><code class="plain plain">sudo yum install php php-gd php-mysql php-mcrypt</code></div>
</div></td>
</tr>
</tbody>
</table>
</div>
</div>
So the above assumes you want MySQL, GD and Mcrypt support in your PHP, but you should see something like the below depending on which version of PHP you are trying to install:
<div>
<div id="highlighter_508682" class="syntaxhighlighter  plain">
<table border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td class="gutter">
<div class="line number1 index0 alt2">1</div>
<div class="line number2 index1 alt1">2</div>
<div class="line number3 index2 alt2">3</div>
<div class="line number4 index3 alt1">4</div>
<div class="line number5 index4 alt2">5</div>
<div class="line number6 index5 alt1">6</div>
<div class="line number7 index6 alt2">7</div>
<div class="line number8 index7 alt1">8</div>
<div class="line number9 index8 alt2">9</div>
<div class="line number10 index9 alt1">10</div>
<div class="line number11 index10 alt2">11</div>
<div class="line number12 index11 alt1">12</div>
<div class="line number13 index12 alt2">13</div>
<div class="line number14 index13 alt1">14</div>
<div class="line number15 index14 alt2">15</div>
<div class="line number16 index15 alt1">16</div>
<div class="line number17 index16 alt2">17</div>
<div class="line number18 index17 alt1">18</div>
<div class="line number19 index18 alt2">19</div>
<div class="line number20 index19 alt1">20</div></td>
<td class="code">
<div class="container">
<div class="line number1 index0 alt2"><code class="plain plain">================================================================================================================================</code></div>
<div class="line number2 index1 alt1"><code class="plain spaces"> </code><code class="plain plain">Package                        Arch                   Version                                 Repository                  Size</code></div>
<div class="line number3 index2 alt2"><code class="plain plain">================================================================================================================================</code></div>
<div class="line number4 index3 alt1"><code class="plain plain">Installing:</code></div>
<div class="line number5 index4 alt2"><code class="plain spaces"> </code><code class="plain plain">php                            x86_64                 5.5.20-2.el6.remi                       remi-php55                 2.6 M</code></div>
<div class="line number6 index5 alt1"><code class="plain spaces"> </code><code class="plain plain">php-gd                         x86_64                 5.5.20-2.el6.remi                       remi-php55                  72 k</code></div>
<div class="line number7 index6 alt2"><code class="plain spaces"> </code><code class="plain plain">php-mysqlnd                    x86_64                 5.5.20-2.el6.remi                       remi-php55                 3.6 M</code></div>
<div class="line number8 index7 alt1"><code class="plain plain">Installing for dependencies:</code></div>
<div class="line number9 index8 alt2"><code class="plain spaces"> </code><code class="plain plain">php-cli                        x86_64                 5.5.20-2.el6.remi                       remi-php55                 3.7 M</code></div>
<div class="line number10 index9 alt1"><code class="plain spaces"> </code><code class="plain plain">php-common                     x86_64                 5.5.20-2.el6.remi                       remi-php55                 1.0 M</code></div>
<div class="line number11 index10 alt2"><code class="plain spaces"> </code><code class="plain plain">php-pdo                        x86_64                 5.5.20-2.el6.remi                       remi-php55                 112 k</code></div>
<div class="line number12 index11 alt1"><code class="plain spaces"> </code><code class="plain plain">php-pear                       noarch                 1:1.9.5-3.el6.remi                      remi                       375 k</code></div>
<div class="line number13 index12 alt2"><code class="plain spaces"> </code><code class="plain plain">php-pecl-jsonc                 x86_64                 1.3.6-1.el6.remi.5.5.1                  remi-php55                  47 k</code></div>
<div class="line number14 index13 alt1"><code class="plain spaces"> </code><code class="plain plain">php-pecl-zip                   x86_64                 1.12.4-1.el6.remi.5.5                   remi-php55                 269 k</code></div>
<div class="line number15 index14 alt2"><code class="plain spaces"> </code><code class="plain plain">php-process                    x86_64                 5.5.20-2.el6.remi                       remi-php55                  57 k</code></div>
<div class="line number16 index15 alt1"><code class="plain spaces"> </code><code class="plain plain">php-xml                        x86_64                 5.5.20-2.el6.remi                       remi-php55                 208 k</code></div>
<div class="line number17 index16 alt2"></div>
<div class="line number18 index17 alt1"><code class="plain plain">Transaction Summary</code></div>
<div class="line number19 index18 alt2"><code class="plain plain">================================================================================================================================</code></div>
<div class="line number20 index19 alt1"><code class="plain plain">Install      11 Package(s)</code></div>
</div></td>
</tr>
</tbody>
</table>
</div>
</div>
As you can see PHP is installing version 5.5.20-2.el6.remi from the remi-php55 repo! Once you have hit Y to confirm the install <strong>restart apache</strong> and magical unicorns you have a better version of PHP!

You can also change your mind in the future by going back into the <code>remi.repo</code> file and enable a different PHP version and then run <code>yum update</code> and if you have moved from 5.5 to 5.6 it will upgrade PHP for you. If you want to downgrade for any reason you will need to remove PHP (<code>sudo yum remove php*</code>) and then reinstall the PHP modules you want.

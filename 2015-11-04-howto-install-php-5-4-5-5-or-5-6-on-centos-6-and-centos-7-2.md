---
layout: post
title: Howto Install PHP 5.4, 5.5 or 5.6 on CentOS 6 and CentOS 7
date: 2015-11-04 09:14
author: administrator
comments: true
categories: [Linux]
---
Repo Installation
Open up a SSH connection to your server and run the following commands (make sure you run as sudo if you need to):

For CentOS 7 (including EPEL install)
1
2
3
wget http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-5.noarch.rpm
wget http://rpms.famillecollet.com/enterprise/remi-release-7.rpm
rpm -Uvh remi-release-7*.rpm epel-release-7*.rpm
If you already have EPEL installed:

1
2
wget http://rpms.famillecollet.com/enterprise/remi-release-7.rpm
rpm -Uvh remi-release-7*.rpm
For CentOS 6 (including EPEL install)
1
2
3
wget http://dl.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm
wget http://rpms.famillecollet.com/enterprise/remi-release-6.rpm
rpm -Uvh remi-release-6*.rpm epel-release-6*.rpm
If you already have EPEL installed:

1
2
wget http://rpms.famillecollet.com/enterprise/remi-release-6.rpm
rpm -Uvh remi-release-6*.rpm
Enabling the Repo
Now we need to make sure the repo is enabled and select which version you want to install. We need to head over to /etc/yum.repos.d you should inside see a file called remi.repo.

Open the file in your favourite editor (Nano, Pico, Vi etc), you’ll see a number of sections. We need to make sure that the first section [remi] is enabled:

1
2
3
4
5
6
7
[remi]
name=Les RPM de remi pour Enterprise Linux 6 - $basearch
#baseurl=http://rpms.famillecollet.com/enterprise/6/remi/$basearch/
mirrorlist=http://rpms.famillecollet.com/enterprise/6/remi/mirror
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-remi
Note the line enabled=1 make sure this is set! Now technically you can actually go ahead and install PHP, but you will only get PHP 5.4.*. Which might be want to you want is so skip ahead to the next section!

If we want PHP 5.5 or PHP 5.6 we need to do a bit more work, further down in the repo.repo file you will see two additional sections [remi-php55] and [remi-php56], decide which PHP version you want to install and then enable the correct. So for PHP 5.6 we would change to:

1
2
3
4
5
6
7
8
[remi-php56]
name=Les RPM de remi de PHP 5.6 pour Enterprise Linux 6 - $basearch
#baseurl=http://rpms.famillecollet.com/enterprise/6/php56/$basearch/
mirrorlist=http://rpms.famillecollet.com/enterprise/6/php56/mirror
# WARNING: If you enable this repository, you must also enable "remi"
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-remi
Once you made your changes save your modified file and quit your editor.

Installing PHP
Now I’m assuming you don’t already have PHP installed, this bit is super simple.

1
sudo yum install php php-gd php-mysql php-mcrypt
So the above assumes you want MySQL, GD and Mcrypt support in your PHP, but you should see something like the below depending on which version of PHP you are trying to install:

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
================================================================================================================================
Package Arch Version Repository Size
================================================================================================================================
Installing:
php x86_64 5.5.20-2.el6.remi remi-php55 2.6 M
php-gd x86_64 5.5.20-2.el6.remi remi-php55 72 k
php-mysqlnd x86_64 5.5.20-2.el6.remi remi-php55 3.6 M
Installing for dependencies:
php-cli x86_64 5.5.20-2.el6.remi remi-php55 3.7 M
php-common x86_64 5.5.20-2.el6.remi remi-php55 1.0 M
php-pdo x86_64 5.5.20-2.el6.remi remi-php55 112 k
php-pear noarch 1:1.9.5-3.el6.remi remi 375 k
php-pecl-jsonc x86_64 1.3.6-1.el6.remi.5.5.1 remi-php55 47 k
php-pecl-zip x86_64 1.12.4-1.el6.remi.5.5 remi-php55 269 k
php-process x86_64 5.5.20-2.el6.remi remi-php55 57 k
php-xml x86_64 5.5.20-2.el6.remi remi-php55 208 k

Transaction Summary
================================================================================================================================
Install 11 Package(s)
As you can see PHP is installing version 5.5.20-2.el6.remi from the remi-php55 repo! Once you have hit Y to confirm the install restart apache and magical unicorns you have a better version of PHP!

You can also change your mind in the future by going back into the remi.repo file and enable a different PHP version and then run yum update and if you have moved from 5.5 to 5.6 it will upgrade PHP for you. If you want to downgrade for any reason you will need to remove PHP (sudo yum remove php*) and then reinstall the PHP modules you want.

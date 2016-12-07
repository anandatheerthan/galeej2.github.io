---
layout: post
title: SAP Data Services  - List All Files Script
date: 2015-11-11 07:08
author: administrator
comments: true
categories: [SAP Data Services]
---
Times you might want to get list of all files within a directory and process them serially using Data Services. This script will come handy in such instances.
<pre class="lang:c decode:true "># define parent folder and file path variables to be used in DIR below
$path_and_file = $input_path || $input_file;
# define target file 
$file_list = $input_path || 'filelist.txt';
# construct the DIR command
$dir_cmd = 'dir [$path_and_file] /b /s /a:-d &gt; [$file_list]';
# pushes results of DIR to a file, use flag 8 to give a return code and
# any messages that appear from the CMD window after completing the DIR
$cmd_return = exec( 'cmd.exe', [$dir_cmd], 8 );
print( $cmd_return );
if ( file_exists( $file_list ) = 1 ) print( 'File list created' );</pre>
You can now use filelist.txt in a file format and populate in data services.

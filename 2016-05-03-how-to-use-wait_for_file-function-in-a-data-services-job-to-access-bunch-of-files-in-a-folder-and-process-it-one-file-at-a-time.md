---
layout: post
title: How to use wait_for_file function in a data services job to access bunch of files in a folder and process it one file at a time?
date: 2016-05-03 11:58
author: administrator
comments: true
categories: [SAP Data Services]
---
The files could be in any location accessible to job server and can access any types of files such as text, csv, xlsx or xml.
<p style="margin: 0in 0in 7.5pt 0in;"><span style="font-size: 16.0pt;">1. Create a batch job in data services designer and declare the following global variables:</span></p>

<pre class="lang:default decode:true ">$file_list - varchar(1000), $list_size - int, $counter - int, 
$file_name - varchar(100), $file_list_temp - varchar(1000)</pre>
<span style="font-size: 16.0pt;">$file_list and $file_list_temp hold comma separated list of absolute paths to the files so the size should be big enough to hold the list. $file_name holds an absolute path to single file.</span>
<p style="box-sizing: border-box; margin: 0in 0in 7.5pt 0in;"><span style="font-size: 16.0pt;">2. Create a startup script as follows:</span></p>

<pre class="lang:default decode:true ">wait_for_file('C:\Program Files (x86)\SAP BusinessObjects\Data Services\dsdata\*.txt', 1, 1, -1,$file_list, $list_size,',');
print('Number of file found = ' || $list_size);
print('Comma separated file list = ' || $file_list);
$file_list_temp = $file_list;</pre>
<span style="font-size: 16.0pt;">The script shows an example of where to look for the files. You can change it according to your system. In this case it looks for all txt files in the folder: C:\Program Files (x86)\SAP BusinessObjects\Data Services\dsdata. If the script runs properly, it will print number of files found and the comma separated list of files with their absolute path. You can tweak polling inteval and other options as desired.</span>
<p style="box-sizing: border-box; margin: 0in 0in 7.5pt 0in;"><span style="font-size: 16.0pt;">3. Add a while loop after the script in the batch job. the while loop condition is:</span></p>

<pre class="lang:default decode:true ">while $counter &lt; $list_size</pre>
<span style="font-size: 16.0pt;">4. Add a script in the while loop as follows. It extracts a single file each time from $file_list using simple string functions. It prints the current file in process and remaining file list at the end.</span>
<pre class="lang:default decode:true ">$counter = $counter + 1;
print('While Loop Counter = ' || $counter );
#print(' comma index = ' || index($file_list , ',', 1));

if($counter = $list_size) 
$file_name= $file_list_temp;
else 
$file_name = substr($file_list_temp , 1, index($file_list, ',',1)-1);
$file_list_temp = substr($file_list_temp, index($file_list,',',1)+1, length($file_list_temp)-index($file_list,',',1));

print('Current file in process is ' || $file_name);
print(' Remaining file list is = '|| $file_list_temp);</pre>
<span style="font-size: 16.0pt;">5. Now you can add a data flow, use the current file for processing. You can also use $file_name to create a flat file format to be used in data flow.</span>

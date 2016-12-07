---
layout: post
title: Retrieve file path of all files within directory in PHP
date: 2015-10-13 04:22
author: administrator
comments: true
categories: [PHP]
---
This script outputs complete file path of all files within specified directory.

&lt;?php

$THE_PATTERN=$_SERVER["DOCUMENT_ROOT"]."/images/*.*";

$TheFilesList = @glob($THE_PATTERN);
$TheFilesTotal = @count($TheFilesList);
$TheFilesTotal = $TheFilesTotal - 1;
$TheFileTemp = "";

for ($TheFilex=0; $TheFilex&lt;=$TheFilesTotal; $TheFilex++)
{
$TheFileTemp = $TheFilesList[$TheFilex];
echo $TheFileTemp . "&lt;br&gt;"; // here you can get full address of files (one by one)
}
?&gt;

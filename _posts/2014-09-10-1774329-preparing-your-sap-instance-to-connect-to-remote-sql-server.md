---
layout: post
title: 1774329 - Preparing your SAP instance to connect to remote SQL server
date: 2014-09-10 15:08
author: administrator
comments: true
categories: [Uncategorized]
---
<div ct="TextView" style="background-color: white; font-family: Arial, Helvetica, sans-serif; font-weight: bold; white-space: nowrap;"><span style="color: #04357b;">Symptom</span></div><div style="background-color: white; font-family: 'Lucida Console', Monaco, 'Courier new', monospace; font-size: 12px;">*************************************************************<br />*&nbsp;&nbsp; The following instructions apply to the Windows<br />*&nbsp;&nbsp; operating environment.<br />*&nbsp;&nbsp; If you are using Linux, then follow the instructions<br />*&nbsp;&nbsp; of note 1644499.<br />****************************************************************<br /><br />You want to configure an SAP application server instance to connect to a remote SQL Server using the DBCON database connectivity method.</div><br style="background-color: white; font-family: Arial, Helvetica, sans-serif;" /><div ct="TextView" style="background-color: white; font-family: Arial, Helvetica, sans-serif; font-weight: bold; white-space: nowrap;"><span style="color: #04357b;">Other Terms</span></div><div style="background-color: white; font-family: 'Lucida Console', Monaco, 'Courier new', monospace; font-size: 12px;"></div><br style="background-color: white; font-family: Arial, Helvetica, sans-serif;" /><div ct="TextView" style="background-color: white; font-family: Arial, Helvetica, sans-serif; font-weight: bold; white-space: nowrap;"><span style="color: #04357b;">Reason and Prerequisites</span></div><div style="background-color: white; font-family: 'Lucida Console', Monaco, 'Courier new', monospace; font-size: 12px;">The application server must run on a Microsoft Windows Server operating system.</div><br style="background-color: white; font-family: Arial, Helvetica, sans-serif;" /><div ct="TextView" style="background-color: white; font-family: Arial, Helvetica, sans-serif; font-weight: bold; white-space: nowrap;"><span style="color: #04357b;">Solution</span></div><div style="background-color: white; font-family: 'Lucida Console', Monaco, 'Courier new', monospace; font-size: 12px;"><b>Obtaining the Required Software</b><br /><br />If your SAP system is installed on Microsoft SQL Server, then your software is already installed.<br /><br />The following section only applies when your SAP System is installed on a different database system than Microsoft SQL Server.<br /><br />To create a connection from the SAP System to a SQL Server, you will need two database system-specific software components.&nbsp;&nbsp;These are the Database Shared Library (DBSL) from SAP and the Microsoft SQL Server SNAC client library. You can download the SAP DBSL from SAP Service Marketplace.&nbsp;&nbsp;The SNAC client can be downloaded from http://download.microsoft.com<br /><br />You only have to set up the DBSL and the SNAC library once if your SAP System runs on a different database platform than SQL Server. Of course, you should also update both software products during your maintenance periods by following the same steps as the initial setup.<br /><b>Downloading the DBSL from the Software Distribution Center on SAP Service Marketplace:</b><br /><br />Open a Web browser and enter the following URL:<br />http://service.sap.com/swdc<br />In the navigation area, choose "Support Packages and Patches" and then "Browse our Download Catalog".<br />In the navigation area, choose:<br />"SAP NetWeaver and complementary products"<br />-&gt; "SAP NetWeaver"<br />-&gt; &lt;Choose your NetWeaver release&gt;<br />-&gt; "Entry by Component"<br />-&gt; "Application Server ABAP"<br />-&gt; &lt;Choose the kernel release of your system&gt;<br />-&gt; "Windows Server &lt;your platform&gt;"<br />-&gt; "MS SQL Server"<br />In the area "Download objects", select the file "lib_dbsl_&lt;patchlevel&gt;-&lt;nnnnnnnn&gt;.sar".<br />Make sure that you select the file with the highest patch level.<br />Download this file to a temporary folder.<br />To unpack the archive, use the program SAPCAR as follows:<br />SAPCAR -xvf lib_dbsl_&lt;patchlevel&gt;-&lt;nnnnnnnn&gt;.sar.<br />After you have successfully unpacked the archive, you no longer require the file lib_dbsl_&lt;patchlevel&gt;-&lt;nnnnnnnn&gt;.sar and you can delete it.<br /><br /><b>Downloading the MS SQL Server SNAC Client Software</b><br /><br />Open a Web browser and enter the following URL:<br /><br />http://download.microsoft.com<br /><br />Normally you want to download SNAC client software which has a release which is equal or higher than the version of the SQL Servers you are connecting to. But in some cases the newest release can no longer connect to older SQL Servers.&nbsp;&nbsp;For example the SQL 2012 SNAC client will not connect to SQL Server 2000.<br /><br />Search on the words "Microsoft SQL Server Feature Pack". Select the latest feature pack found, and scroll down to select the proper Microsoft SQL Server Native Client.&nbsp;&nbsp;Download the proper sqlncli.msi for your platform.<br /><br />The SQL Server 2008 client can connect to SQL Server 2008, SQL Server 2005 and SQL Server 2000 servers.<br /><br />The SQL Server 2012 client can connect to SQL Server 2012, SQL Server 2008 and SQL Server 2005.<br /><br /><b>Installing the Software</b><br /><br />The SNAC software is installed by running the sqlncli.msi file downloaded from the Microsoft website.<br /><br />The DBSL dbmssslib.dll file is installed by moving it to the DIR_EXECUTABLE of your application server. You can check the location of this directory by running report RSPFPAR for example.&nbsp;&nbsp;The current value for DIR_EXECUTABLE can be seen by choosing the row and pressing F2.<br /><b>Updating the Client Software</b><br /><br />When you install a SNAC client it has a release version tied to a specific SQL Server release. As you patch the SQL Server Database Engine with Microsoft Service Packs, you should also patch the SNAC Client.<br /><br />For example, when you install the first release of SQL Server it is referred to as SQL Server 2012 RTM ("Release to Manufacturing"). The SNAC client installed at that time would also be the SQL Server 2012 SNAC RTM version. When you patch the database engine of SQL Server 2012 with Service Pack 1, you should also patch the SNAC client to SQL Server 2012 SNAC Service Pack 1 on any server which connects to the newly patched database.<br /></div><br style="background-color: white; font-family: Arial, Helvetica, sans-serif;" /><a href="https://www.blogger.com/null" name="anchor_DEFAULT_HEADER_C" style="background-color: white; font-family: Arial, Helvetica, sans-serif;"></a><br /><div ct="TextView" style="background-color: white; color: #ff7800; font-family: Arial, Helvetica, sans-serif; font-weight: bold; white-space: nowrap;">Header Data</div><table border="0" cellpadding="0" cellspacing="0" ct="MatrixLayout" style="background-color: white; font-family: Arial, Helvetica, sans-serif;"><tbody><tr><td style="padding: 2px 4px 2px 0px;"></td><td style="padding: 2px 4px 2px 0px;"><span style="zoom: 1;"></span></td></tr><tr><td style="padding: 2px 4px 2px 0px;"><span ct="TextView" style="font-size: 0.7em; font-weight: bold; white-space: nowrap;">Released On</span></td><td style="padding: 2px 4px 2px 0px;"><span ct="TextView" style="font-size: 0.7em; white-space: nowrap;">16.10.2012 20:40:20</span></td></tr><tr><td style="padding: 2px 4px 2px 0px;"><span ct="TextView" style="font-size: 0.7em; font-weight: bold; white-space: nowrap;">Release Status</span></td><td style="padding: 2px 4px 2px 0px;"><span ct="TextView" style="font-size: 0.7em; white-space: nowrap;">Released for Customer</span></td></tr><tr><td style="padding: 2px 4px 2px 0px;"><span ct="TextView" style="font-size: 0.7em; font-weight: bold; white-space: nowrap;">Component</span></td><td style="padding: 2px 4px 2px 0px;"><span ct="TextView" style="font-size: 0.7em; white-space: nowrap;">BC-DB-MSS Microsoft SQL Server</span></td></tr><tr><td style="padding: 2px 4px 2px 0px;"><span ct="TextView" style="font-size: 0.7em; font-weight: bold; white-space: nowrap;">Priority</span></td><td style="padding: 2px 4px 2px 0px;"><span ct="TextView" style="font-size: 0.7em; white-space: nowrap;">Recommendations / Additional Info</span></td></tr><tr><td style="padding: 2px 4px 2px 0px;"><span ct="TextView" style="font-size: 0.7em; font-weight: bold; white-space: nowrap;">Category</span></td><td style="padding: 2px 4px 2px 0px;"><span ct="TextView" style="font-size: 0.7em; white-space: nowrap;">FAQ</span></td></tr></tbody></table><a href="https://www.blogger.com/null" name="anchor_CORR_VALIDITY_C" style="background-color: white; font-family: Arial, Helvetica, sans-serif;"></a><br style="background-color: white; font-family: Arial, Helvetica, sans-serif;" /><div ct="TextView" style="background-color: white; color: #ff7800; font-family: Arial, Helvetica, sans-serif; font-weight: bold; white-space: nowrap;">Validity</div><span ct="TextView" style="background-color: white; font-family: Arial, Helvetica, sans-serif; font-size: 0.7em;">This document is not restricted to a software component or software component version</span><span style="background-color: white; font-family: Arial, Helvetica, sans-serif;">&nbsp;</span><a href="https://www.blogger.com/null" name="anchor_DEFAULT_GR_C" style="background-color: white; font-family: Arial, Helvetica, sans-serif;"></a><br /><div ct="TextView" style="background-color: white; color: #ff7800; font-family: Arial, Helvetica, sans-serif; font-weight: bold; white-space: nowrap;">References</div><div ct="TextView" style="background-color: white; font-family: Arial, Helvetica, sans-serif; font-size: 0.8em; font-weight: bold; white-space: nowrap;">This document refers to:</div><span ct="TextView" style="background-color: white; color: #666666; font-family: Arial, Helvetica, sans-serif; font-size: 0.7em; font-weight: bold; white-space: nowrap;">SAP Notes</span><span style="background-color: white; font-family: Arial, Helvetica, sans-serif;"></span><br /><table style="background-color: white; font-family: Arial, Helvetica, sans-serif;"><tbody><tr><td align="right"><span ct="TextView" style="font-size: 0.7em; white-space: nowrap;">1781460</span></td><td>&nbsp;</td><td><a ct="Link" href="https://websmp230.sap-ag.de/sap/support/notes/1781460" style="color: #756183; cursor: pointer;" target="_blank"><span style="cursor: pointer; font-size: 0.7em; vertical-align: middle;">Client unable to establish connection to SQL Server 2000</span></a></td></tr><tr><td align="right"><span ct="TextView" style="font-size: 0.7em; white-space: nowrap;">1644499</span></td><td>&nbsp;</td><td><a ct="Link" href="https://websmp230.sap-ag.de/sap/support/notes/1644499" style="color: #756183; cursor: pointer;" target="_blank"><span style="cursor: pointer; font-size: 0.7em; vertical-align: middle;">Database connectivity from Linux to SQL Server</span></a></td></tr><tr><td align="right"><span ct="TextView" style="font-size: 0.7em; white-space: nowrap;">1458291</span></td><td>&nbsp;</td><td><a ct="Link" href="https://websmp230.sap-ag.de/sap/support/notes/1458291" style="color: #756183; cursor: pointer;" target="_blank"><span style="cursor: pointer; font-size: 0.7em; vertical-align: middle;">SolMan 7.1 Database Warehouse &amp; Alerting for MSSQL</span></a></td></tr><tr><td align="right"><span ct="TextView" style="font-size: 0.7em; white-space: nowrap;">1388700</span></td><td>&nbsp;</td><td><a ct="Link" href="https://websmp230.sap-ag.de/sap/support/notes/1388700" style="color: #756183; cursor: pointer;" target="_blank"><span style="cursor: pointer; font-size: 0.7em; vertical-align: middle;">SolMan 7.0 EHP1 Database Warehouse for MSSQL</span></a></td></tr><tr><td align="right"><span ct="TextView" style="font-size: 0.7em; white-space: nowrap;">1316740</span></td><td>&nbsp;</td><td><a ct="Link" href="https://websmp230.sap-ag.de/sap/support/notes/1316740" style="color: #756183; cursor: pointer;" target="_blank"><span style="cursor: pointer; font-size: 0.7em; vertical-align: middle;">Set up remote monitoring for Microsoft SQL Server databases</span></a></td></tr><tr><td align="right"><span ct="TextView" style="font-size: 0.7em; white-space: nowrap;">178949</span></td><td>&nbsp;</td><td><a ct="Link" href="https://websmp230.sap-ag.de/sap/support/notes/178949" style="color: #756183; cursor: pointer;" target="_blank"><span style="cursor: pointer; font-size: 0.7em; vertical-align: middle;">MSSQL: Database MultiConnect</span></a></td></tr></tbody></table><div ct="TextView" style="background-color: white; font-family: Arial, Helvetica, sans-serif; font-size: 0.8em; font-weight: bold; white-space: nowrap;">This document is referenced by:</div><span ct="TextView" style="background-color: white; color: #666666; font-family: Arial, Helvetica, sans-serif; font-size: 0.7em; font-weight: bold; white-space: nowrap;">SAP Notes (7)</span><span style="background-color: white; font-family: Arial, Helvetica, sans-serif;"></span><br /><table style="background-color: white; font-family: Arial, Helvetica, sans-serif;"><tbody><tr><td><span ct="TextView" style="font-size: 0.7em; white-space: nowrap;">178949</span></td><td>&nbsp;</td><td><a ct="Link" href="https://websmp230.sap-ag.de/sap/support/notes/178949" style="color: #756183; cursor: pointer;" target="_blank"><span style="cursor: pointer; font-size: 0.7em; vertical-align: middle;">MSSQL: Database MultiConnect</span></a></td></tr><tr><td><span ct="TextView" style="font-size: 0.7em; white-space: nowrap;">1316740</span></td><td>&nbsp;</td><td><a ct="Link" href="https://websmp230.sap-ag.de/sap/support/notes/1316740" style="color: #756183; cursor: pointer;" target="_blank"><span style="cursor: pointer; font-size: 0.7em; vertical-align: middle;">Set up remote monitoring for Microsoft SQL Server databases</span></a></td></tr><tr><td><span ct="TextView" style="font-size: 0.7em; white-space: nowrap;">1458291</span></td><td>&nbsp;</td><td><a ct="Link" href="https://websmp230.sap-ag.de/sap/support/notes/1458291" style="color: #756183; cursor: pointer;" target="_blank"><span style="cursor: pointer; font-size: 0.7em; vertical-align: middle;">SolMan 7.1 Database Warehouse &amp; Alerting for MSSQL</span></a></td></tr><tr><td><span ct="TextView" style="font-size: 0.7em; white-space: nowrap;">1388700</span></td><td>&nbsp;</td><td><a ct="Link" href="https://websmp230.sap-ag.de/sap/support/notes/1388700" style="color: #756183; cursor: pointer;" target="_blank"><span style="cursor: pointer; font-size: 0.7em; vertical-align: middle;">SolMan 7.0 EHP1 Database Warehouse for MSSQL</span></a></td></tr><tr><td><span ct="TextView" style="font-size: 0.7em; white-space: nowrap;">1644499</span></td><td>&nbsp;</td><td><a ct="Link" href="https://websmp230.sap-ag.de/sap/support/notes/1644499" style="color: #756183; cursor: pointer;" target="_blank"><span style="cursor: pointer; font-size: 0.7em; vertical-align: middle;">Database connectivity from Linux to SQL Server</span></a></td></tr><tr><td><span ct="TextView" style="font-size: 0.7em; white-space: nowrap;">1781460</span></td><td>&nbsp;</td><td><a ct="Link" href="https://websmp230.sap-ag.de/sap/support/notes/1781460" style="color: #756183; cursor: pointer;" target="_blank"><span style="cursor: pointer; font-size: 0.7em; vertical-align: middle;">Client unable to establish connection to SQL Server 2000</span></a></td></tr><tr><td><span ct="TextView" style="font-size: 0.7em; white-space: nowrap;">1954407</span></td><td>&nbsp;</td><td><span style="color: #756183; cursor: pointer; font-size: 0.7em; vertical-align: middle;"><a ct="Link" href="https://websmp230.sap-ag.de/sap/support/notes/1954407" style="color: #756183; cursor: pointer;" target="_blank">DBCON connections using Windows logins for SQL Server</a><br /></span></td></tr></tbody></table>
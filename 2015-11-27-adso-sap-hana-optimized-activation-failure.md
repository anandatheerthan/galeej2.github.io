---
layout: post
title: ADSO - SAP HANA Optimized Activation Failure
date: 2015-11-27 01:25
author: administrator
comments: true
categories: [HANA, SAP BW]
---
If you receive activation error while activating request in ADSO, you may try the below.<a href="http://www.rsa1.xyz/wp-content/uploads/2015/11/Capture1.png"><img class="alignnone size-medium wp-image-444" src="http://www.rsa1.xyz/wp-content/uploads/2015/11/Capture1-300x41.png" alt="Capture" width="300" height="41" /></a>
<ol>
	<li>Set CLIENT_DISTRIBUTION_MODE = OFF in HANA Studio</li>
	<li>Change the HDBuserstore entry to have master node on first position, so that ABAP stack always connects with Master Node.</li>
</ol>

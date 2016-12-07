---
layout: post
title: Delete Inactive transformation from SAP BW Production
date: 2015-11-17 03:19
author: administrator
comments: true
categories: [SAP BW]
---
Using the class CL_RSTRAN_STAT and the method DELETE_VERSION_FROM_DB ,we can delete the transformation that is inactive in the system.

Input is transformation id and version = 'M'

---
layout: post
title: BI7 WAD and the underlying BEX queries
date: 2012-10-16 05:08
author: administrator
comments: true
categories: [SAP BW]
---
By using the below tables , you can get list of all queries used in BI 7 WAD.
<h6><span style="text-decoration: underline;">Tables</span></h6>
&nbsp;
<h6>RSZWBTMPXREF
RSZWBTMPHEAD
RSZWBTMPHEADTXT
RSZCOMPDIR
RSZCOMPIC
RSZELTTXT</h6>
<strong><span style="text-decoration: underline;">Join Conditions</span></strong>

RSZWBTMPXREF OBJNM = RSZCOMPDIR COMPUID
RSZWBTMPXREF OBJVERS = RSZCOMPDIR OBJVERS
RSZWBTMPXREF OBJID = RSZWBTMPHEAD OBJID
RSZWBTMPXREF OBJVERS = RSZWBTMPHEAD OBJVERS
RSZWBTMPHEAD OBJID = RSZWBTMPHEADTXT OBJID
RSZWBTMPHEAD OBJVERS = RSZWBTMPHEADTXT OBJVERS
RSZCOMPDIR COMPUID = RSZCOMPIC COMPUID
RSZCOMPDIR OBJVERS = RSZCOMPIC OBJVERS
RSZCOMPDIR COMPUID = RSZELTTXT ELTUID
RSZCOMPDIR OBJVERS = RSZELTTXT OBJVERS

<span style="color: #000000;"><strong><span style="text-decoration: underline;"><span style="text-decoration: underline;">Filter</span></span></strong></span>

RSZWBTMPXREF OBJVERS EQ 'A'
RSZWBTMPXREF TLOGO EQ 'ELEM'
RSZWBTMPHEADTXT LANGU EQ 'E'
RSZELTTXT LANGU EQ 'E'

<span style="text-decoration: underline;"><strong>Output Fields</strong></span>

WADOBJID
WADTXTLG
INFOCUBE
QRYCOMPID
QRYTXTLG
QRYCOMPUID
LAST_CHANGE_BY

---
layout: post
title: Reading Field Symbol Internal Table in ABAP
date: 2016-05-13 18:11
author: administrator
comments: true
categories: [ABAP]
---
<pre class="lang:default decode:true ">data: field type string.
field = 'MANDT'.
READ TABLE &lt;any_tab&gt; ASSIGNING &lt;any_wa&gt; WITH KEY (field) = '800'. 
IF sy-subrc = 0.
  "do stuff with &lt;any_wa&gt;...
ENDIF.</pre>
&nbsp;

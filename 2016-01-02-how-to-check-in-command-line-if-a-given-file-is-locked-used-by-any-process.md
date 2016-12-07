---
layout: post
title: How to check in command-line if a given file is locked (used by any process)?
date: 2016-01-02 18:27
author: administrator
comments: true
categories: [SAP Data Services]
---
When you use wait_for_file to trigger job upon file placement, there are chances that the file is locked because it is used by some other process or the file being copied is in progress. You can use below script in data services to check for such conditions and trigger the job if necessary.
<pre><code>2&gt;nul (
  &gt;&gt;test.txt (call )
) &amp;&amp; (echo file is not locked) || (echo file is locked)</code></pre>

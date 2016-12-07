---
layout: post
title: Delete data from table based on another table
date: 2015-09-11 04:16
author: administrator
comments: true
categories: [SQL]
---
<pre class="lang-sql prettyprint prettyprinted"><code><span class="kwd">DELETE</span> <span class="kwd">FROM</span><span class="pln"> t1 </span><span class="kwd">USING</span><span class="pln"> table1 t1 </span><span class="kwd">INNER</span> <span class="kwd">JOIN</span><span class="pln"> table2 t2 </span><span class="kwd">ON</span> <span class="pun">(</span><span class="pln"> t1</span><span class="pun">.</span><span class="kwd">group</span> <span class="pun">=</span><span class="pln"> t2</span><span class="pun">.</span><span class="kwd">group</span> <span class="pun">);</span></code></pre>

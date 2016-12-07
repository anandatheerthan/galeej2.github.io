---
layout: post
title: Update Query based on Select Query in MySql
date: 2015-01-22 14:09
author: administrator
comments: true
categories: [MySql]
---
AN sample below to write an update query that should be executed based on a select query and conditions.
<pre class="lang-sql prettyprint prettyprinted"><code><span class="kwd">update</span><span class="pln"> tableA a
</span><span class="kwd">left</span> <span class="kwd">join</span><span class="pln"> tableB b </span><span class="kwd">on</span><span class="pln">
    a</span><span class="pun">.</span><span class="pln">name_a </span><span class="pun">=</span><span class="pln"> b</span><span class="pun">.</span><span class="pln">name_b
</span><span class="kwd">set</span><span class="pln">
    validation_check </span><span class="pun">=</span> <span class="kwd">if</span><span class="pun">(</span><span class="pln">start_dts </span><span class="pun">&gt;</span><span class="pln"> end_dts</span><span class="pun">,</span> <span class="str">'VALID'</span><span class="pun">,</span> <span class="str">''</span><span class="pun">)</span></code></pre>

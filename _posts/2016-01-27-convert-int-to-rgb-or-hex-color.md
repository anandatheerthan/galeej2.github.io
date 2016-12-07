---
layout: post
title: Convert int to RGB or hex color
date: 2016-01-27 15:01
author: administrator
comments: true
categories: [SQL]
---
<pre class="lang-sql prettyprint prettyprinted"><code><span class="kwd">SELECT</span> 
    <span class="str">'#'</span>
    <span class="pun">+</span> <span class="kwd">CONVERT</span><span class="pun">(</span><span class="pln">varchar</span><span class="pun">(</span><span class="lit">6</span><span class="pun">),</span><span class="pln">
        CAST</span><span class="pun">(</span><span class="pln">ABS</span><span class="pun">(@</span><span class="pln">color</span><span class="pun">)</span> <span class="kwd">as</span><span class="pln"> varbinary</span><span class="pun">(</span><span class="lit">1</span><span class="pun">))</span>
        <span class="pun">+</span><span class="pln">CAST</span><span class="pun">(</span><span class="pln">ABS</span><span class="pun">(@</span><span class="pln">color</span><span class="pun">/</span><span class="lit">256</span><span class="pun">)</span> <span class="kwd">as</span><span class="pln"> varbinary</span><span class="pun">(</span><span class="lit">1</span><span class="pun">))</span>
        <span class="pun">+</span><span class="pln">CAST</span><span class="pun">(</span><span class="pln">ABS</span><span class="pun">(@</span><span class="pln">color</span><span class="pun">/</span><span class="lit">256</span><span class="pun">/</span><span class="lit">256</span><span class="pun">)</span> <span class="kwd">as</span><span class="pln"> varbinary</span><span class="pun">(</span><span class="lit">1</span><span class="pun">))</span>
    <span class="pun">,</span> <span class="lit">2</span><span class="pun">)</span></code></pre>

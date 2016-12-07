---
layout: post
title: Did you know about havingRaw() function?
date: 2016-06-16 12:19
author: administrator
comments: true
categories: [Laravel]
---
Eloquent and Query Builder have a lot of “hidden gems” which are not in the official docs. For example, if you want to perform GROUP BY and HAVING, there’s a little trick for unnamed columns.

Let’s say you want to filter all product categories with more than one products – which means write this query in Eloquent:
<div id="crayon-576299083cc0f820817689" class="crayon-syntax crayon-theme-twilight crayon-font-monaco crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-mouseover">
<div class="crayon-main">
<pre class="lang:default decode:true ">SELECT *, COUNT(*) FROM products GROUP BY category_id HAVING count(*) &gt; 1
</pre>
</div>
</div>
Basically, it’s simple – you would just use <b>groupBy()</b> and <b>having()</b>functions, right? But we don’t have the column name for <em>having</em>. Of course, we can assign it, and with Query Builder write something like:
<div id="crayon-576299083cc22189686425" class="crayon-syntax crayon-theme-twilight crayon-font-monaco crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-mouseover">
<div class="crayon-plain-wrap"></div>
<div class="crayon-main">
<table class="crayon-table">
<tbody>
<tr class="crayon-row">
<td class="crayon-nums " data-settings="show">
<div class="crayon-nums-content">
<div class="crayon-num" data-line="crayon-576299083cc22189686425-1"></div>
</div></td>
<td class="crayon-code">
<div class="crayon-pre">
<div id="crayon-576299083cc22189686425-1" class="crayon-line">
<pre class="lang:default decode:true ">DB::table('products')
    -&gt;select('*', DB::raw('COUNT(*) as products_count'))
    -&gt;groupBy('category_id')
    -&gt;having('products_count', '&gt;' , 1)
    -&gt;get();</pre>
</div>
</div></td>
</tr>
</tbody>
</table>
</div>
</div>
But there’s a shorter way – there’s a function <b>havingRaw()</b>:
<div id="crayon-576299083cc2a735905265" class="crayon-syntax crayon-theme-twilight crayon-font-monaco crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-mouseover">
<div class="crayon-main">
<pre class="lang:default decode:true  ">Product::groupBy('category_id')-&gt;havingRaw('COUNT(*) &gt; 1')-&gt;get();</pre>
</div>
</div>
You can add your wanted columns into <b>select()</b>, but essentially that’s a shortcut I wanted to briefly show you.

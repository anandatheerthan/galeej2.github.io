---
layout: post
title: How to fix “this file type is not permitted for security reasons” in WordPress
date: 2015-12-09 05:45
author: administrator
comments: true
categories: [PHP]
---
In WordPress, files with certain extensions (e.g., .exe, .bz2, .zip) are forbidden to upload to the media library for security reasons. This security feature is known as "filtered upload." In some cases, however, you may want to override this default security policy, and allow some file types which are otherwise blacklisted. In fact, there are ways to disable or customize file type blacklist in WordPress.
<h2>Allow All File Types in File Upload</h2>
If you want to turn off filtered upload policy altogether, so that you can upload arbitrary types of files to WordPress, do the following.

Open <tt>wp-config.php</tt> of your WordPress site with any text editor, and add the following line somewhere in the file.
<div>
<div id="highlighter_994936" class="syntaxhighlighter  php">
<table border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td class="gutter">
<div class="line number1 index0 alt2">1</div></td>
<td class="code">
<div class="container">
<div class="line number1 index0 alt2"><code class="php plain">define(</code><code class="php string">'ALLOW_UNFILTERED_UPLOADS'</code><code class="php plain">, true);</code></div>
</div></td>
</tr>
</tbody>
</table>
</div>
</div>
This will turn off file-type filter during file uploading on WordPress.
<h2>Enable File Upload for a Specific File Type</h2>
If you want to be able to upload files with a specific file extension which is otherwise blocked by default, add the following code in <tt>functions.php</tt> of your WordPress theme.
<div>
<div id="highlighter_878201" class="syntaxhighlighter  php">
<table border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td class="gutter">
<div class="line number1 index0 alt2">1</div>
<div class="line number2 index1 alt1">2</div>
<div class="line number3 index2 alt2">3</div>
<div class="line number4 index3 alt1">4</div>
<div class="line number5 index4 alt2">5</div>
<div class="line number6 index5 alt1">6</div>
<div class="line number7 index6 alt2">7</div>
<div class="line number8 index7 alt1">8</div>
<div class="line number9 index8 alt2">9</div>
<div class="line number10 index9 alt1">10</div>
<div class="line number11 index10 alt2">11</div>
<div class="line number12 index11 alt1">12</div>
<div class="line number13 index12 alt2">13</div>
<div class="line number14 index13 alt1">14</div>
<div class="line number15 index14 alt2">15</div>
<div class="line number16 index15 alt1">16</div>
<div class="line number17 index16 alt2">17</div>
<div class="line number18 index17 alt1">18</div>
<div class="line number19 index18 alt2">19</div>
<div class="line number20 index19 alt1">20</div></td>
<td class="code">
<div class="container">
<div class="line number1 index0 alt2"><code class="php keyword">function</code> <code class="php plain">enable_extended_upload ( </code><code class="php variable">$mime_types</code> <code class="php plain">=</code><code class="php keyword">array</code><code class="php plain">() ) {</code></div>
<div class="line number2 index1 alt1"></div>
<div class="line number3 index2 alt2"><code class="php spaces">   </code><code class="php comments">// The MIME types listed here will be allowed in the media library.</code></div>
<div class="line number4 index3 alt1"><code class="php spaces">   </code><code class="php comments">// You can add as many MIME types as you want.</code></div>
<div class="line number5 index4 alt2"><code class="php spaces">   </code><code class="php variable">$mime_types</code><code class="php plain">[</code><code class="php string">'gz'</code><code class="php plain">]  = </code><code class="php string">'application/x-gzip'</code><code class="php plain">;</code></div>
<div class="line number6 index5 alt1"><code class="php spaces">   </code><code class="php variable">$mime_types</code><code class="php plain">[</code><code class="php string">'zip'</code><code class="php plain">]  = </code><code class="php string">'application/zip'</code><code class="php plain">;</code></div>
<div class="line number7 index6 alt2"><code class="php spaces">   </code><code class="php variable">$mime_types</code><code class="php plain">[</code><code class="php string">'rtf'</code><code class="php plain">] = </code><code class="php string">'application/rtf'</code><code class="php plain">;</code></div>
<div class="line number8 index7 alt1"><code class="php spaces">   </code><code class="php variable">$mime_types</code><code class="php plain">[</code><code class="php string">'ppt'</code><code class="php plain">] = </code><code class="php string">'application/mspowerpoint'</code><code class="php plain">;</code></div>
<div class="line number9 index8 alt2"><code class="php spaces">   </code><code class="php variable">$mime_types</code><code class="php plain">[</code><code class="php string">'ps'</code><code class="php plain">] = </code><code class="php string">'application/postscript'</code><code class="php plain">;</code></div>
<div class="line number10 index9 alt1"><code class="php spaces">   </code><code class="php variable">$mime_types</code><code class="php plain">[</code><code class="php string">'flv'</code><code class="php plain">] = </code><code class="php string">'video/x-flv'</code><code class="php plain">;</code></div>
<div class="line number11 index10 alt2"></div>
<div class="line number12 index11 alt1"><code class="php spaces">   </code><code class="php comments">// If you want to forbid specific file types which are otherwise allowed,</code></div>
<div class="line number13 index12 alt2"><code class="php spaces">   </code><code class="php comments">// specify them here.  You can add as many as possible.</code></div>
<div class="line number14 index13 alt1"><code class="php spaces">   </code><code class="php plain">unset( </code><code class="php variable">$mime_types</code><code class="php plain">[</code><code class="php string">'exe'</code><code class="php plain">] );</code></div>
<div class="line number15 index14 alt2"><code class="php spaces">   </code><code class="php plain">unset( </code><code class="php variable">$mime_types</code><code class="php plain">[</code><code class="php string">'bin'</code><code class="php plain">] );</code></div>
<div class="line number16 index15 alt1"></div>
<div class="line number17 index16 alt2"><code class="php spaces">   </code><code class="php keyword">return</code> <code class="php variable">$mime_types</code><code class="php plain">;</code></div>
<div class="line number18 index17 alt1"><code class="php plain">}</code></div>
<div class="line number19 index18 alt2"></div>
<div class="line number20 index19 alt1"><code class="php plain">add_filter(</code><code class="php string">'upload_mimes'</code><code class="php plain">, </code><code class="php string">'enable_extended_upload'</code><code class="php plain">);</code></div>
</div></td>
</tr>
</tbody>
</table>
</div>
</div>

---
layout: post
title: Basic File Uploading Using PHP
date: 2014-10-15 11:58
author: administrator
comments: true
categories: [PHP]
---
I create a lot of websites that allow administrators to upload files to their own website. Since allowing user customization has become more and more important on websites these days, I thought I'd share how easy it is to handle file uploads in PHP.
<h2>The XHTML Form</h2>
<pre class=" language-html"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>form</span> <span class="token attr-name">action</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>accept-file.php<span class="token punctuation">"</span></span> <span class="token attr-name">method</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>post<span class="token punctuation">"</span></span> <span class="token attr-name">enctype</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>multipart/form-data<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
	Your Photo: <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>input</span> <span class="token attr-name">type</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>file<span class="token punctuation">"</span></span> <span class="token attr-name">name</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>photo<span class="token punctuation">"</span></span> <span class="token attr-name">size</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>25<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
	<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>input</span> <span class="token attr-name">type</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>submit<span class="token punctuation">"</span></span> <span class="token attr-name">name</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>submit<span class="token punctuation">"</span></span> <span class="token attr-name">value</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>Submit<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>form</span><span class="token punctuation">&gt;</span></span></pre>
You'll need to use the <span class="parameter">multipart/form-data</span> value for the form's <span class="parameter">enctype</span> property. You'll also obviously need at least one input element of the <span class="parameter">file</span> type. The form's action tag must provide a URL which points the a file containing the piece of PHP below.
<h2>The PHP</h2>
<pre class=" language-php"><span class="token comment" spellcheck="true">//if they DID upload a file...
</span><span class="token keyword">if</span><span class="token punctuation">(</span><span class="token global">$_FILES</span><span class="token punctuation">[</span><span class="token string">'photo'</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token string">'name'</span><span class="token punctuation">]</span><span class="token punctuation">)</span>
<span class="token punctuation">{</span>
<span class="token comment" spellcheck="true">	//if no errors...
</span>	<span class="token keyword">if</span><span class="token punctuation">(</span><span class="token operator">!</span><span class="token global">$_FILES</span><span class="token punctuation">[</span><span class="token string">'photo'</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token string">'error'</span><span class="token punctuation">]</span><span class="token punctuation">)</span>
	<span class="token punctuation">{</span>
	<span class="token comment" spellcheck="true">	//now is the time to modify the future file name and validate the file
</span>		<span class="token variable">$new_file_name</span> <span class="token operator">=</span> <span class="token function">strtolower<span class="token punctuation">(</span></span><span class="token global">$_FILES</span><span class="token punctuation">[</span><span class="token string">'photo'</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token string">'tmp_name'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span><span class="token comment" spellcheck="true"> //rename file
</span>		<span class="token keyword">if</span><span class="token punctuation">(</span><span class="token global">$_FILES</span><span class="token punctuation">[</span><span class="token string">'photo'</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token string">'size'</span><span class="token punctuation">]</span> <span class="token operator">&gt;</span> <span class="token punctuation">(</span><span class="token number">1024000</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token comment" spellcheck="true"> //can't be larger than 1 MB
</span>		<span class="token punctuation">{</span>
			<span class="token variable">$valid_file</span> <span class="token operator">=</span> <span class="token boolean">false</span><span class="token punctuation">;</span>
			<span class="token variable">$message</span> <span class="token operator">=</span> <span class="token string">'Oops!  Your file's size is to large.'</span><span class="token punctuation">;</span>
		<span class="token punctuation">}</span>
		
	<span class="token comment" spellcheck="true">	//if the file has passed the test
</span>		<span class="token keyword">if</span><span class="token punctuation">(</span><span class="token variable">$valid_file</span><span class="token punctuation">)</span>
		<span class="token punctuation">{</span>
		<span class="token comment" spellcheck="true">	//move it to where we want it to be
</span>			<span class="token function">move_uploaded_file<span class="token punctuation">(</span></span><span class="token global">$_FILES</span><span class="token punctuation">[</span><span class="token string">'photo'</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token string">'tmp_name'</span><span class="token punctuation">]</span><span class="token punctuation">,</span> <span class="token string">'uploads/'</span><span class="token punctuation">.</span><span class="token variable">$new_file_name</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
			<span class="token variable">$message</span> <span class="token operator">=</span> <span class="token string">'Congratulations!  Your file was accepted.'</span><span class="token punctuation">;</span>
		<span class="token punctuation">}</span>
	<span class="token punctuation">}</span>
<span class="token comment" spellcheck="true">	//if there is an error...
</span>	<span class="token keyword">else</span>
	<span class="token punctuation">{</span>
	<span class="token comment" spellcheck="true">	//set that to be the returned message
</span>		<span class="token variable">$message</span> <span class="token operator">=</span> <span class="token string">'Ooops!  Your upload triggered the following error:  '</span><span class="token punctuation">.</span><span class="token global">$_FILES</span><span class="token punctuation">[</span><span class="token string">'photo'</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token string">'error'</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>
<span class="token comment" spellcheck="true">
//you get the following information for each file:
</span><span class="token global">$_FILES</span><span class="token punctuation">[</span><span class="token string">'field_name'</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token string">'name'</span><span class="token punctuation">]</span>
<span class="token global">$_FILES</span><span class="token punctuation">[</span><span class="token string">'field_name'</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token string">'size'</span><span class="token punctuation">]</span>
<span class="token global">$_FILES</span><span class="token punctuation">[</span><span class="token string">'field_name'</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token string">'type'</span><span class="token punctuation">]</span>
<span class="token global">$_FILES</span><span class="token punctuation">[</span><span class="token string">'field_name'</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token string">'tmp_name'</span><span class="token punctuation">]</span></pre>
My commenting in the PHP above outlines the way the process works, so I'll just mention a few notes about file uploads in PHP:
<ul>
	<li>Many shared hosting servers allow a very low maximum file upload size. If you plan on accepting larger files, you should consider a dedicated or virtual dedicated server.</li>
	<li>To adjust the file upload size in PHP, modify the <span class="file">php.ini</span> file's "upload_max_filesize" value. You can also adjust this value using PHP's <span class="function">.ini_set()</span> function.</li>
	<li>The file upload counts towards the hosting environment's <span class="var">$_POST</span> size, so you may need to increase the <span class="file">php.ini</span> file's <span class="parameter">post_max_size</span> value.</li>
	<li>Be sure to do a lot of file validation when allowing users to upload files. How horrible would it be to allow a user to upload a <span class="file">.exe</span> file to your server? They could do horrible things on the server.</li>
</ul>

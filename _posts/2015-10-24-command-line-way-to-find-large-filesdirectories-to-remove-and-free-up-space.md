---
layout: post
title: Command line way to find large files/directories to remove and free up space
date: 2015-10-24 13:27
author: administrator
comments: true
categories: [Linux]
---
If you just need to find large files, you can use <code>find</code> with the <code>-size</code> option. Additionally you can use sort command to sort the output.The next command will list all files larger than 10MiB (MB is not same as MiB):
<pre><code>find / -size +10M -ls
</code></pre>
If you want to find files between a certain size, you can combine it with a "size lower than" search. The next command find files between 10MiB and 12MiB:
<pre><code>find / -size +10M -size -12M -ls</code></pre>

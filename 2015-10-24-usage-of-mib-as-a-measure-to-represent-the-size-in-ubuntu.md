---
layout: post
title: Usage of "MiB" as a measure to represent the size in Ubuntu
date: 2015-10-24 13:24
author: administrator
comments: true
categories: [Linux]
---
There are two ways (in common use) of denoting orders of magnitude to make large numbers easier to read, first you can use a power of 10.
<pre><code>10⁰ = 1
10¹ = 10
10² = 100
10³ = 1000
</code></pre>
Or powers of two
<pre><code>2⁰ = 1
2¹ = 2
2² = 4
2³ = 8
</code></pre>
Using these series as a base we arrive at the numbers 1000 and 1024 (10³ and 2¹⁰) for a <em>kilo</em>.

There are eight bits to a byte. So one kilobyte is 8×10³ = 8000 bits. Hard drive manufacturers use this method. In computer science, people usually use powers of two, so one kibibyte is 8×2¹⁰ = 8192 bits.

The difference only gets larger as the numbers get larger. Some have even mixed those two systems to get nice numbers to put on their packaging. This is why a 1.44MB floppy disk has neither 1.44 megabytes nor 1.44 mebibytes (they use 1024×1000).

The <em>logic behind the i</em> is that the terms are derived from the original si prefixes, kilo, mega, giga, but with the word <em>binary</em> put in in. So the <em>i</em> is the second letter of <em>binary</em>. The mnemonic for the kibibyte is "kilo binary byte", and "KiB" is pronounced "Kibibyte".

All of this is defined in the <a href="http://en.wikipedia.org/wiki/IEC_80000">IEC_80000 Standard</a>.

Note that a mebibyte is not defined as 2²⁰, but as (2<sup>10</sup>)<sup><sup>2</sup></sup>, although they are equal. A gibibyte is (2<sup>10</sup>)<sup><sup>3</sup></sup>, a tebibyte is (2<sup>10</sup>)<sup><sup>4</sup></sup> and so on.
<pre><code>Prefix       Bytes                      Prefix       Bytes
1 Byte     = (2^10)^0 = 1               1 Byte     = (10^3)^0 = 1
1 Kibibyte = (2^10)^1 = 1024            1 Kilobyte = (10^3)^1 = 1000
1 Mebibyte = (2^10)^2 = 1048576         1 Megabyte = (10^3)^2 = 1000000
1 Gibibyte = (2^10)^3 = 1073741824      1 Gigabyte = (10^3)^3 = 1000000000
1 Tebibyte = (2^10)^4 = 1099511627776   1 Terabyte = (10^3)^4 = 1000000000000
</code></pre>
Keep in mind that, <em>very often,</em> the term kilobyte is used when the author means kibibyte. The binary unit was only introduced around 1999, as Randy Orrison points out.

<hr />

As <strong>nealmcb</strong> found out in the comments, there is an official policy on this:
<a href="https://wiki.ubuntu.com/UnitsPolicy">https://wiki.ubuntu.com/UnitsPolicy</a>

In summary, this policy reminds developers to either use SI or IEC prefixes, but to never mix them. It goes on to say:
<blockquote>For file sizes there are two possibilities:
<ul>
	<li>Show both, base-10 and base-2 (in this order). An example is the Linux kernel: "2930277168 512-byte hardware sectors: (1.50 TB/1.36 TiB)"</li>
	<li>Only show base-10, or give the user the opportunity to decide between base-10 and base-2 (the default must be base-10).</li>
</ul>
</blockquote>

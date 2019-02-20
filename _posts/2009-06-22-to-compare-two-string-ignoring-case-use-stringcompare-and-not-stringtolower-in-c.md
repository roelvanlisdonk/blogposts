---
ID: 566
post_title: 'To compare two string, ignoring case, use string.Compare and not string.ToLower in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/06/22/to-compare-two-string-ignoring-case-use-stringcompare-and-not-stringtolower-in-c/
published: true
post_date: 2009-06-22 11:33:10
---
<p>If you want to compare two string, ignoring case, use string.Compare and not string.ToLower, for performance reasons.   <br />    <br /></p>  <pre class="code"><span style="color: blue">if </span>(<span style="color: blue">string</span>.Compare(stringA, stringA, <span style="color: blue">true</span>) == 0)<br />{</pre>

<pre class="code">    // Strings are equal (case ignored)<br /><br />}</pre>
<a href="http://11011.net/software/vspaste"></a>
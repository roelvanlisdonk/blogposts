---
ID: 1041
post_title: 'How to determine if a given path is a relative path in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/02/24/how-to-determine-if-a-given-path-is-a-relative-path-in-c/
published: true
post_date: 2010-02-24 07:41:42
---
<p>If you want to determine if a given path is a relative path in C#, you can use the System.IO.Path.IsPathRooted function:</p>  <pre class="code"><span style="color: blue">bool </span>isPathRooted = <span style="color: #2b91af">Path</span>.IsPathRooted(<span style="color: #a31515">&quot;Test.txt&quot;</span>);

<span style="color: #2b91af">Console</span>.WriteLine(isPathRooted);</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>Result: False</p>

<pre class="code"><span style="color: blue">bool </span>isPathRooted = <span style="color: #2b91af">Path</span>.IsPathRooted(<span style="color: #a31515">@&quot;\\nas\Test.txt&quot;</span>);

<span style="color: #2b91af">Console</span>.WriteLine(isPathRooted);</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>Result: True</p>

<pre class="code"><span style="color: blue">bool </span>isPathRooted = <span style="color: #2b91af">Path</span>.IsPathRooted(<span style="color: #a31515">@&quot;C:\Test.txt&quot;</span>);

<span style="color: #2b91af">Console</span>.WriteLine(isPathRooted);</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>Result: True</p>
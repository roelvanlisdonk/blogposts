---
ID: 1162
post_title: 'How to make sure the first character of a string is one slash &lsquo;/&rsquo; with C#, use the TrimStart function'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/29/how-to-make-sure-the-first-character-of-a-string-is-one-slash-with-c-use-the-trimstart-function/
published: true
post_date: 2010-03-29 11:54:46
---
<p>If you want to make sure the first character of a string is one slash, use the function:</p>  <pre class="code"><span style="color: blue">public string </span>PrependPath(<span style="color: blue">string </span>path, <span style="color: blue">string </span>firstCharacter)
{
<span style="color: blue">    return </span>firstCharacter + path.TrimStart(firstCharacter.ToCharArray());
}</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p>To test the function use:</p>

<pre class="code"><span style="color: blue">string </span>firstCharacter = <span style="color: #a31515">&quot;/&quot;</span>;
<span style="color: #2b91af">Console</span>.WriteLine(PrependPath(<span style="color: #a31515">&quot;TestPath&quot;</span>, firstCharacter));
<span style="color: #2b91af">Console</span>.WriteLine(PrependPath(<span style="color: #a31515">&quot;/TestPath&quot;</span>, firstCharacter));
<span style="color: #2b91af">Console</span>.WriteLine(PrependPath(<span style="color: #a31515">&quot;//TestPath&quot;</span>, firstCharacter));
<span style="color: #2b91af">Console</span>.WriteLine(PrependPath(<span style="color: #a31515">&quot;///TestPath&quot;</span>, firstCharacter));    </pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p><strong>Result </strong></p>

<p>/TestPath
  <br />/TestPath

  <br />/TestPath

  <br />/TestPath</p>
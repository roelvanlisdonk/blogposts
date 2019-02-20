---
ID: 258
post_title: >
  Use string.Format to handle strings that
  are empty or null
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/02/11/use-stringformat-to-handle-strings-that-are-empty-or-null/
published: true
post_date: 2009-02-11 14:07:46
---
<pre class="code"><span style="color:#2b91af;">Console</span>.WriteLine(<span style="color:blue;">string</span>.Format(<span style="color:#a31515;">"{0} [{1}]"</span>, <span style="color:#a31515;">"object1"</span>, <span style="color:blue;">null</span>));</pre><a href="http://11011.net/software/vspaste"></a>Result:<br />
<p>object1 []</p>
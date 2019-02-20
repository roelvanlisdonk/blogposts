---
ID: 538
post_title: 'C# &#8211; Assert that a string is not null or empty with NUnit'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/06/12/c-assert-that-a-string-is-not-null-or-empty-with-nunit/
published: true
post_date: 2009-06-12 09:44:20
---
If you want to Assert that a result string in a NUnit test is not null or empty, use:   <pre class="code"><span style="color: #2b91af">Assert</span>.That(<span style="color: blue">string</span>.IsNullOrEmpty(result), <span style="color: #2b91af">Is</span>.False, <span style="color: #a31515">&quot;Result string must not be null or empty&quot;</span>);</pre>
<a href="http://11011.net/software/vspaste"></a>
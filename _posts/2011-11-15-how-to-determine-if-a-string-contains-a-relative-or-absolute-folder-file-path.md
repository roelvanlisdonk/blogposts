---
ID: 2209
post_title: 'How to determine if a string contains a relative or absolute folder / file path in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/11/15/how-to-determine-if-a-string-contains-a-relative-or-absolute-folder-file-path/
published: true
post_date: 2011-11-15 10:51:26
---
<p>&#160;</p>  <p>If you want to determine if a string contains a relative or absolute folder / file path, you can use the System.IO.Path.IsPathRooted function:</p>  <pre class="code"><span style="color: #2b91af">Console</span>.WriteLine(System.IO.<span style="color: #2b91af">Path</span>.IsPathRooted(<span style="color: #a31515">@&quot;..\Test.cs&quot;</span>)); <span style="color: green">// Result: False
</span><span style="color: #2b91af">Console</span>.WriteLine(System.IO.<span style="color: #2b91af">Path</span>.IsPathRooted(<span style="color: #a31515">@&quot;C:\Test.cs&quot;</span>)); <span style="color: green">// Result: True
</span></pre>
---
ID: 854
post_title: 'Replace XElement with xml in string (C#)'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/12/15/replace-xelement-with-xml-in-string-c/
published: true
post_date: 2009-12-15 14:32:41
---
<p>If you want to replace an existing XElement by an new XElement conctructed from a string, you can use the XElement ReplaceWith method:</p>  <pre class="code"><span style="color: #2b91af">           XElement </span>element = <span style="color: blue">new </span><span style="color: #2b91af">XElement</span>(<span style="color: #a31515">&quot;MyName&quot;</span>, <span style="color: #a31515">&quot;MyContent&quot;</span>);
           <span style="color: blue">string </span>newValue = <span style="color: #a31515">&quot;&lt;MyNewName&gt;Some value&lt;/MyNewName&gt;&quot;</span>;
           element.ReplaceWith(<span style="color: #2b91af">XElement</span>.Parse(newValue));</pre>
<a href="http://11011.net/software/vspaste"></a>
---
ID: 710
post_title: >
  How to convert a string containing XML
  to XDocument
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/09/18/how-to-convert-a-string-containing-xml-to-xdocument/
published: true
post_date: 2009-09-18 12:56:48
---
<p>If you want to convert a string containing XML to a XDocument object, use:</p>  <pre class="code"><span style="color: blue">var </span>document = <span style="color: #2b91af">XDocument</span>.Parse(<span style="color: #a31515">@&quot;&lt;?xml version=&quot;&quot;1.0&quot;&quot;?&gt;&lt;root&gt;&lt;/root&gt;&quot;</span>);</pre>

<p>For converting XmlDocument to XDocument and vice versa, see: <a title="http://blogs.msdn.com/marcelolr/archive/2009/03/13/fast-way-to-convert-xmldocument-into-xdocument.aspx" href="http://blogs.msdn.com/marcelolr/archive/2009/03/13/fast-way-to-convert-xmldocument-into-xdocument.aspx">http://blogs.msdn.com/marcelolr/archive/2009/03/13/fast-way-to-convert-xmldocument-into-xdocument.aspx</a></p>
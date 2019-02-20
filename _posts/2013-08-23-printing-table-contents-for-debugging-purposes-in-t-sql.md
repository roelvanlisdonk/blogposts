---
ID: 3340
post_title: >
  Printing table contents for debugging
  purposes in T-SQL
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/08/23/printing-table-contents-for-debugging-purposes-in-t-sql/
published: true
post_date: 2013-08-23 10:30:24
---
<p>Sometimes you just want to add a print statement in a stored procedure to output the contents of a table.</p>  <p>Then you can use the &quot;FOR XML&quot; statement in T-SQL:</p>  <pre class="code"><span style="color: blue">declare </span><span style="color: teal">@Data_as_xml </span><span style="color: blue">xml
set </span><span style="color: teal">@Data_as_xml </span><span style="color: gray">= (</span><span style="color: blue">select top </span>4 <span style="color: gray">* </span><span style="color: blue">from </span><span style="color: green">sys</span><span style="color: gray">.</span><span style="color: green">tables </span><span style="color: blue">FOR XML PATH</span><span style="color: gray">(</span><span style="color: red">''</span><span style="color: gray">))
</span><span style="color: blue">print </span><span style="color: magenta">convert</span><span style="color: gray">(</span><span style="color: blue">varchar</span><span style="color: gray">(</span>8000<span style="color: gray">), </span><span style="color: teal">@Data_as_xml</span><span style="color: gray">)
</span></pre>

<p>Result:</p>

<p>&#160;</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/08/image2.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/08/image_thumb2.png" width="580" height="150" /></a></p>
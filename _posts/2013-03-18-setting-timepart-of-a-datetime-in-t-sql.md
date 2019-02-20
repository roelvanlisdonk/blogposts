---
ID: 3178
post_title: Setting timepart of a datetime in T-SQL
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/03/18/setting-timepart-of-a-datetime-in-t-sql/
published: true
post_date: 2013-03-18 07:09:58
---
<p>&#160;</p>   <pre class="code"><span style="color: blue">select </span><span style="color: magenta">cast</span><span style="color: gray">((</span><span style="color: magenta">substring</span><span style="color: gray">(</span><span style="color: magenta">convert</span><span style="color: gray">(</span><span style="color: blue">varchar</span><span style="color: gray">, </span><span style="color: magenta">getdate</span><span style="color: gray">() , </span>20<span style="color: gray">), </span>0<span style="color: gray">, </span>12<span style="color: gray">) + </span><span style="color: red">'10:00:00'</span><span style="color: gray">) </span><span style="color: blue">as datetime</span><span style="color: gray">)
</span></pre>
---
ID: 3181
post_title: >
  How to left pad a string in T-SQL (SQL
  Server 2012)
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/04/03/how-to-left-pad-a-string-in-t-sql-sql-server-2012/
published: true
post_date: 2013-04-03 13:55:25
---
<p>If you want to left pad a string in T-SQL in Microsoft SQL Server 2012, you can use the format function:</p>  <p>To get the current hour padded with, zeros use:</p>  <pre class="code"><span style="color: blue">declare </span><span style="color: teal">@CurrentDateTime </span><span style="color: blue">datetime </span><span style="color: gray">= </span><span style="color: red">'2013-04-03 05:06:17'
</span><span style="color: blue">select </span><span style="color: magenta">format</span><span style="color: gray">(</span><span style="color: magenta">datepart</span><span style="color: gray">(</span><span style="color: teal">hh</span><span style="color: gray">, </span><span style="color: teal">@CurrentDateTime</span><span style="color: gray">), </span><span style="color: red">'00'</span><span style="color: gray">)

</span><span style="color: green">-- Result: 05
</span></pre>

<p>For more information, including (SQL 2005, and 2008 options):</p>

<p><a href="http://www.tech-recipes.com/rx/30469/sql-server-how-to-left-pad-a-number-with-zeros/">http://www.tech-recipes.com/rx/30469/sql-server-how-to-left-pad-a-number-with-zeros/</a></p>
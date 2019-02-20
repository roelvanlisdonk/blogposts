---
ID: 515
post_title: >
  Return all rows with TSQL when a
  Microsoft Reporting Services parameter
  is null
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/06/04/return-all-rows-with-tsql-when-a-microsoft-reporting-services-parameter-is-null/
published: true
post_date: 2009-06-04 20:44:58
---
<p>This examples uses the Microsoft SQL Server 2008 example database AdventureWorks (<a href="http://msftdbprodsamples.codeplex.com/">http://msftdbprodsamples.codeplex.com/</a>)</p> If you want to return all rows of a table when a parameter is null, use the TSQL function isnull:   <br />  <br />  <br />  <pre class="code"><span style="color: blue">declare </span>@productModelID <span style="color: blue">as int
set </span>@productModelID <span style="color: gray">= null


</span><span style="color: blue">select
    </span>p<span style="color: gray">.*
</span><span style="color: blue">from
    </span>Production<span style="color: gray">.</span>Product p
<span style="color: blue">where
    </span><span style="color: magenta">isnull</span><span style="color: gray">(</span>@productModelID<span style="color: gray">, </span>p<span style="color: gray">.</span>ProductModelID<span style="color: gray">) = </span>p<span style="color: gray">.</span>ProductModelID
<span style="color: blue">order by </span>p<span style="color: gray">.</span>ProductID</pre>
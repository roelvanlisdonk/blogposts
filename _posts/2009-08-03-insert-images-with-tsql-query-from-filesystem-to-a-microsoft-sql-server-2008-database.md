---
ID: 590
post_title: >
  Insert images with TSQL query from
  filesystem to a Microsoft SQL Server
  2008 database
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/08/03/insert-images-with-tsql-query-from-filesystem-to-a-microsoft-sql-server-2008-database/
published: true
post_date: 2009-08-03 08:42:45
---
<p>To insert a image from filesystem to a Microsoft SQL Server 2008 database with a TSQL query, use:   <br /></p>  <pre class="code"><span style="color: blue">INSERT INTO </span>MyTable<span style="color: gray">(</span>MyImageColumn<span style="color: gray">)
</span><span style="color: blue">SELECT </span><span style="color: gray">* </span><span style="color: blue">FROM
OPENROWSET</span><span style="color: gray">(</span><span style="color: blue">BULK </span><span style="color: red">N'C:\Image1.jpg'</span><span style="color: gray">, </span><span style="color: blue">SINGLE_BLOB</span><span style="color: gray">)</span></pre>
<a href="http://11011.net/software/vspaste"></a>
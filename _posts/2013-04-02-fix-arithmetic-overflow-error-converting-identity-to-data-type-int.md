---
ID: 3180
post_title: 'Fix: Arithmetic overflow error converting IDENTITY to data type int'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/04/02/fix-arithmetic-overflow-error-converting-identity-to-data-type-int/
published: true
post_date: 2013-04-02 11:12:24
---
<p>I was getting the error: &quot;Arithmetic overflow error converting IDENTITY to data type int&quot;, when inserting a record in a table with a identity column. The max id of this table was 45448, this is certainly not the max of int in SQL Server, so I expected the next Id to be 45449, but DBCC CHECKIDENT returned 2147483647 (the max of an int).&#160; </p>  <pre class="code"><span style="color: blue">DBCC </span><span style="color: teal">CHECKIDENT </span><span style="color: gray">(</span><span style="color: red">'Reporting.MyTable'</span><span style="color: gray">);
</span></pre>


<p>Reseeding the table with DBCC CHECKIDENT fixed the problem:</p>

<pre class="code"><span style="color: blue">DBCC </span><span style="color: teal">CHECKIDENT </span><span style="color: gray">(</span><span style="color: red">'Reporting.MyTable'</span><span style="color: gray">, </span><span style="color: teal">reseed</span><span style="color: gray">, 45449</span><span style="color: gray">)
</span></pre>
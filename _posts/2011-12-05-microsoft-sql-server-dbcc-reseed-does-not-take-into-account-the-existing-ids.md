---
ID: 2261
post_title: 'Microsoft SQL Server DBCC reseed does not take into account the existing ID&rsquo;s'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/12/05/microsoft-sql-server-dbcc-reseed-does-not-take-into-account-the-existing-ids/
published: true
post_date: 2011-12-05 20:23:54
---
<p>A colleague of mine (Mattijs ter Heijde) created a simple script to verify Microsoft SQL Server DBCC RESEED does not take existing ID’s into account, here’s the T-SQL Code:</p><pre class="code"><span style="color: blue">create table #test </span><span style="color: gray">(id </span><span style="color: blue">int </span><span style="color: gray">not null </span><span style="color: blue">identity</span><span style="color: gray">(1,1) </span><span style="color: blue">primary key</span><span style="color: gray">, t </span><span style="color: blue">int</span><span style="color: gray">)
</span><span style="color: blue">insert #test</span><span style="color: gray">(t) </span><span style="color: blue">values</span><span style="color: gray">(1) </span><span style="color: green">-- Id = 1
</span><span style="color: blue">insert #test</span><span style="color: gray">(t) </span><span style="color: blue">values</span><span style="color: gray">(1) </span><span style="color: green">-- Id = 2
</span><span style="color: blue">insert #test</span><span style="color: gray">(t) </span><span style="color: blue">values</span><span style="color: gray">(1) </span><span style="color: green">-- Id = 3
</span><span style="color: blue">delete #test where Id </span><span style="color: gray">in (1, 2) – </span><span style="color: green">Delete Id 1 and 2
</span><span style="color: blue">dbcc checkident </span><span style="color: gray">(#test, reseed, 0) – </span><span style="color: green">DBCC RESEED

</span><span style="color: blue">insert #test</span><span style="color: gray">(t) </span><span style="color: blue">values</span><span style="color: gray">(1) </span><span style="color: green">-- Id = 1
</span><span style="color: blue">insert #test</span><span style="color: gray">(t) </span><span style="color: blue">values</span><span style="color: gray">(1) </span><span style="color: green">-- Id = 2
</span><span style="color: blue">insert #test</span><span style="color: gray">(t) </span><span style="color: blue">values</span><span style="color: gray">(1) </span><span style="color: green">-- Id = 3 BOOM!!!!!!!!

</span><span style="color: blue">drop table #test
</pre></span>
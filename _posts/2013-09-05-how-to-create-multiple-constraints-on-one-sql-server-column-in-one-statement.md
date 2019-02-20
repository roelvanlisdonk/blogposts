---
ID: 3381
post_title: >
  How to create multiple constraints on
  one SQL Server column in one statement.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/09/05/how-to-create-multiple-constraints-on-one-sql-server-column-in-one-statement/
published: true
post_date: 2013-09-05 11:58:58
---
<p>If you want to add a column to a table in SQL Server and the column should contain multiple constraints, you can declare these constraints inline in one statement by separating them with spaces.</p>  <pre class="code"><span style="color: blue">if </span><span style="color: gray">not exists (</span><span style="color: blue">select </span>1 <span style="color: blue">from </span><span style="color: green">sys</span><span style="color: gray">.</span><span style="color: green">columns </span><span style="color: blue">where </span><span style="color: teal">name </span><span style="color: gray">= </span><span style="color: red">'MyColumn1' </span><span style="color: gray">and </span><span style="color: magenta">Object_ID </span><span style="color: gray">= </span><span style="color: magenta">Object_ID</span><span style="color: gray">(</span><span style="color: red">'dbo.MyTable1'</span><span style="color: gray">))
</span><span style="color: blue">begin 
    alter table </span><span style="color: teal">dbo</span><span style="color: gray">.</span><span style="color: teal">MyTable1 </span><span style="color: blue">with nocheck add </span><span style="color: teal">MyTable2Id </span><span style="color: blue">int </span><span style="color: gray">not null 
        </span><span style="color: blue">constraint </span><span style="color: teal">FK_dbo_MyTable1_MyTable2Id </span><span style="color: blue">foreign key references </span><span style="color: teal">dbo</span><span style="color: gray">.</span><span style="color: teal">MyTable2Id</span><span style="color: gray">(</span><span style="color: teal">Id</span><span style="color: gray">)
        </span><span style="color: blue">constraint </span><span style="color: teal">DF_dbo_MyTable1_MyTable2Id </span><span style="color: blue">default</span><span style="color: gray">(</span>1<span style="color: gray">)
</span><span style="color: blue">end
go
</span></pre>
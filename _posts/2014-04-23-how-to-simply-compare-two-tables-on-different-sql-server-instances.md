---
ID: 3738
post_title: >
  How to simply compare two tables on
  different SQL Server instances.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/04/23/how-to-simply-compare-two-tables-on-different-sql-server-instances/
published: true
post_date: 2014-04-23 08:52:07
---
<p>I restored a backup of a database on a different SQL Server instance running on the same server and I wanted to compare data in a table found on SQL Server Instance 1 with the same table on SQL Server Instance 2.</p>  <p>&#160;</p>  <p>First add a linked server (all queries will be run from [MyServer\MyInstance1])</p>  <pre class="code"><span style="color: blue">exec </span><span style="color: maroon">sp_addlinkedserver </span>@server <span style="color: gray">= </span><span style="color: red">'MyServer\MyInstance2'
</span><span style="color: blue">go
</span></pre>
Then compare the data in the two tables with a except statement:

<p>&#160;</p>

<pre class="code"><span style="color: blue">select </span><span style="color: gray">* </span><span style="color: blue">from </span>[MyServer\MyInstance1]<span style="color: gray">.</span>MyDatabase1<span style="color: gray">.</span>dbo<span style="color: gray">.</span>MyTable1
<span style="color: blue">except
select </span><span style="color: gray">* </span><span style="color: blue">from </span>[MyServer\MyInstance2]<span style="color: gray">.</span>MyDatabase1<span style="color: gray">.</span>dbo<span style="color: gray">.</span>MyTable1</pre>
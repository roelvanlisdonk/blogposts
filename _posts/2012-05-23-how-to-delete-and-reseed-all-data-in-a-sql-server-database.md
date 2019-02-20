---
ID: 2701
post_title: >
  How to delete and reseed all data in a
  SQL Server database
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/05/23/how-to-delete-and-reseed-all-data-in-a-sql-server-database/
published: true
post_date: 2012-05-23 09:56:50
---
<p>If you want to delete all data in a SQL Server database and reseed the tables that contain a identity column, you can use the following code:</p>  <pre class="code"><span style="color: blue">exec </span><span style="color: maroon">sp_msforeachtable </span><span style="color: teal">&quot;alter table ? nocheck constraint all&quot;</span><span style="color: gray">;
</span><span style="color: blue">exec </span><span style="color: maroon">sp_msforeachtable </span><span style="color: teal">&quot;delete from ?&quot;</span><span style="color: gray">;
</span><span style="color: blue">exec </span><span style="color: maroon">sp_msforeachtable </span><span style="color: teal">&quot;if exists(select 1 from sys.identity_columns where object_name(object_id) = '?') begin dbcc checkident ( '?', reseed, 0) end&quot;</span><span style="color: gray">;
</span><span style="color: blue">exec </span><span style="color: maroon">sp_msforeachtable </span><span style="color: teal">&quot;alter table ? with check check constraint all&quot;</span><span style="color: gray">;
</span></pre>
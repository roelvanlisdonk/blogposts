---
ID: 2110
post_title: >
  Drop all connections to a SQL Server
  database with T-SQL
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/07/01/drop-all-connections-to-a-sql-server-database-with-t-sql/
published: true
post_date: 2011-07-01 16:24:08
---
<p>If you want to drop all connections to a database by using T-SQL, connect Microsoft SQL Server Management Studio to the master database, open a new query editor window and execute the following T-SQL code:</p> <p>&nbsp;</p><pre class="code"><span style="color: green">/*
    Drop all connections to a database
*/

-- Take database offline
</span><span style="color: blue">alter database [MyDatabase]
set offline with rollback immediate

</span><span style="color: green">-- Take database online
</span><span style="color: blue">alter database [MyDatabase]
set online
</pre></span>
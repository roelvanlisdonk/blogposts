---
ID: 595
post_title: >
  How to check if column exists in SQL
  Server table
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/08/04/how-to-check-if-column-exists-in-sql-server-table/
published: true
post_date: 2009-08-04 10:29:56
---
SQL Server 2005 onwards:

<span style="color: blue;">if </span><span style="color: gray;">not exists(</span><span style="color: blue;">select 1</span><span style="color: gray;"> </span><span style="color: blue;">from </span><span style="color: green;">sys</span><span style="color: gray;">.</span><span style="color: green;">columns </span><span style="color: blue;">where </span>Name <span style="color: gray;">= </span><span style="color: red;">N'columnName' </span><span style="color: gray;">and </span><span style="color: magenta;">Object_ID </span><span style="color: gray;">= </span><span style="color: magenta;">Object_ID</span><span style="color: gray;">(</span><span style="color: red;">N'tableName'</span><span style="color: gray;">))
</span><span style="color: blue;">begin
    </span><span style="color: green;">-- Column does not exist
</span><span style="color: blue;">end</span>

<a title="http://stackoverflow.com/questions/133031/how-to-check-if-column-exists-in-sql-server-table" href="http://stackoverflow.com/questions/133031/how-to-check-if-column-exists-in-sql-server-table">http://stackoverflow.com/questions/133031/how-to-check-if-column-exists-in-sql-server-table</a>
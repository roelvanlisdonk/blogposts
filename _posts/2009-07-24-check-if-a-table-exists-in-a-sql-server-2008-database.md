---
ID: 580
post_title: >
  Check if a table exists in a SQL Server
  2008 database
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/07/24/check-if-a-table-exists-in-a-sql-server-2008-database/
published: true
post_date: 2009-07-24 12:08:53
---
To check if a table exists in a SQL Server 2008 database, use the following T-SQL code:
Use the system view sys.objects and not the old sql server 2000 system table sysobjects

<span style="color: blue;">
if </span><span style="color: gray;">not exists (</span><span style="color: blue;">select </span>1 <span style="color: blue;">from </span><span style="color: green;">sys.objects </span>o <span style="color: blue;">where </span>o<span style="color: gray;">.</span>name <span style="color: gray;">='</span><span style="color: red;">TableName' </span><span style="color: gray;">and </span>o<span style="color: gray;">.</span>type <span style="color: gray;">='</span><span style="color: red;">U'</span><span style="color: gray;">)
</span><span style="color: blue;">begin
    create table</span>dbo<span style="color: gray;">.</span>TableName <span style="color: gray;">(
       </span>Id <span style="color: blue;">int identity</span><span style="color: gray;">(</span>1<span style="color: gray;">,</span>1<span style="color: gray;">) not null</span><span style="color: blue;">primary key</span><span style="color: gray;">,
       </span>Barcode <span style="color: blue;">varchar</span><span style="color: gray;">(</span>35<span style="color: gray;">) not null</span>
<pre class="code"><span style="color: gray;"> </span><span style="color: gray;">    )
</span><span style="color: blue;">end
</span>go</pre>
<a href="http://11011.net/software/vspaste"></a>
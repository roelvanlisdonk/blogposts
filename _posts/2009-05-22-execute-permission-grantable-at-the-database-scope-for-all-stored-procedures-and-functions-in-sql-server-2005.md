---
ID: 461
post_title: >
  EXECUTE permission grantable at the
  database scope for all stored procedures
  and functions in SQL Server 2005
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/22/execute-permission-grantable-at-the-database-scope-for-all-stored-procedures-and-functions-in-sql-server-2005/
published: true
post_date: 2009-05-22 15:29:16
---
<p>See: <a href="http://www.sqldbatips.com/showarticle.asp?ID=8">http://www.sqldbatips.com/showarticle.asp?ID=8</a></p>  <p>In SQL Server 2000 we had to grand execute rights to all stored procedures by altering the create scripts or executing a sql query like:    <br />declare @sql nvarchar(4000)     <br />declare @db&#160; sysname ; set @db = DB_NAME()     <br />declare @u&#160;&#160; sysname ; set @u = QUOTENAME('&lt;insert_username&gt;')     <br />set @sql ='select ''grant exec on '' + QUOTENAME(ROUTINE_SCHEMA) + ''.'' +     <br />QUOTENAME(ROUTINE_NAME) + '' TO ' + @u + ''' FROM INFORMATION_SCHEMA.ROUTINES ' +     <br />'WHERE OBJECTPROPERTY(OBJECT_ID(ROUTINE_NAME),''IsMSShipped'') = 0'     <br />exec master.dbo.xp_execresultset @sql,@db     <br />In SQL Server 2005 we can grant execute rights to a role instead of a stored procedure:</p>  <pre>/* CREATE A NEW ROLE */
CREATE ROLE db_executor

/* GRANT EXECUTE TO THE ROLE */
GRANT EXECUTE TO db_executor</pre>
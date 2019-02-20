---
ID: 1740
post_title: >
  How to enable SQL Service Broker on a
  SQL Server 2005 database to allow
  SqlCacheDependency
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/09/24/how-to-enable-sql-service-broker-on-a-sql-server-2005-database-to-allow-sqlcachedependency/
published: true
post_date: 2010-09-24 13:12:32
---
<p>If you are using SqlCacheDependency in you’re ASP .NET website, the database must have SQL Server Broker enabled. To enable SQL Server Broker on a SQL Server 2005 database use:</p>  <pre class="code"><span style="color: blue">USE master
</span>GO

<span style="color: blue">ALTER DATABASE </span>Dagstaten <span style="color: blue">SET ENABLE_BROKER  WITH ROLLBACK </span>IMMEDIATE 
GO</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>The set enable_broker requires an exclusive lock on the database, so use “with rollback immediate”.</p>
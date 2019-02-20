---
ID: 1677
post_title: >
  Close sessions (connection) to a
  Microsoft SQL Server instance, from
  other users with TSQL
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/08/23/close-sessions-connection-from-other-users-with-tsql/
published: true
post_date: 2010-08-23 16:13:00
---
<p>If you want to close all connections to a database, you can use the following TSQL code:</p>  <p>&#160;</p>  <p>USE MyDatabase   <br />GO    <br />ALTER DATABASE MyDatabase SET SINGLE_USER WITH ROLLBACK IMMEDIATE    <br />GO    <br />-- Set some options or do some work    <br />GO    <br />ALTER DATABASE MyDatabase SET MULTI_USER    <br />GO</p>
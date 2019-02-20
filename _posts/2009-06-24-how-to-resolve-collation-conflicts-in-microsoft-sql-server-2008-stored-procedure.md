---
ID: 574
post_title: >
  How to resolve collation conflicts in
  Microsoft SQL Server 2008 stored
  procedure
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/06/24/how-to-resolve-collation-conflicts-in-microsoft-sql-server-2008-stored-procedure/
published: true
post_date: 2009-06-24 10:57:37
---
<p>To resolve collation conflicts like: </p>  <p>Msg 468, Level 16, State 9, Line 135   <br />Cannot resolve the collation conflict between &quot;SQL_Latin1_General_CP1_CI_AS&quot; and &quot;Latin1_General_CI_AS&quot; in the equal to operation.</p>  <p>   <br />You should surround the ‘=’ with <span style="color: blue">collate </span>database_default</p>  <p><span style="color: blue">select </span><span style="color: gray">* </span><span style="color: blue">from </span>Product p    <br /><span style="color: gray">inner join </span>Sales s    <br /><span style="color: blue">where </span>p<span style="color: gray">.</span>Name <span style="color: blue">collate </span>database_default <span style="color: gray">= </span>s<span style="color: gray">.</span>ProductName <span style="color: blue">collate </span>database_default</p> <a href="http://11011.net/software/vspaste"></a>  <p>   <br />Solution found at: <a title="http://blog.sqlauthority.com/2007/06/11/sql-server-cannot-resolve-collation-conflict-for-equal-to-operation/" href="http://blog.sqlauthority.com/2007/06/11/sql-server-cannot-resolve-collation-conflict-for-equal-to-operation/">http://blog.sqlauthority.com/2007/06/11/sql-server-cannot-resolve-collation-conflict-for-equal-to-operation/</a></p>
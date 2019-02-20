---
ID: 369
post_title: Stop all SQL Server 2008 BI services
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/11/stop-all-sql-server-2008-bi-services/
published: true
post_date: 2009-05-11 13:31:34
---
<p>net stop "MSSQLServerOLAPService"<br />net stop "MsDtsServer100"<br />net stop "ReportServer"<br />net stop "MSSQLFDLauncher"</p>
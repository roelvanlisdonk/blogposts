---
ID: 529
post_title: 'To connect to a Microsoft SQL Server database with &#8220;Windows Authentication&#8221; from outside the domain use runas /netonly /user:DOMAIN\username'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/06/10/to-connect-to-a-microsoft-sql-server-database-with-windows-authentication-from-outside-the-domain-use-runas-netonly-userdomainusername/
published: true
post_date: 2009-06-10 14:25:48
---
<p>If you have a development VMware image, which is not a member of the domain hosting you’re database, you can still make use of “windows authentication” by running the database script or Microsoft SQL Server Manger as a domain user.   <br />c:\&gt;runas /netonly /user:domain\user &quot;C:\Program Files\Microsoft SQL Server\90\Tools\Binn\VSShell\Common7\IDE\SqlWb.exe&quot;    <br />    <br />To run a database installation bat file, that uses sqlcmd.exe to execute *.sql scripts, use:    <br />c:\&gt;runas /netonly /user:domain\user &quot;cmd”</p>  <p>In the commandlinedialog execute you’re bat file:   <br />C:\Projects\Test&gt;DatabaseInstallation.cmd TestDomain\ONTW1_2008 TestDatabase TestDomain    </p>
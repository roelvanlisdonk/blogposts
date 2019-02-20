---
ID: 520
post_title: '&#8220;Run as&#8221; in Microsoft Windows Vista and Microsoft Windows 2008'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/06/09/run-as-in-microsoft-windows-vista-and-microsoft-windows-2008/
published: true
post_date: 2009-06-09 15:48:42
---
<p>To run a program as another user, you can’t right click the program and choose “Run as…”   <br />To run a program like the Microsoft SQL Server Mangement Studio 2008 with another user credentials:</p>  <p>   <br /> start &gt; run &gt; cmd &gt; runas /user:DevMoss200904\srvTest &quot;C:\Program Files (x86)\Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE\Ssms.exe&quot;    <br />Enter the password for DevMoss200904\srvTest:    <br />    <br />After entering the password the program should start with the given credentials, in this way you can test Windows Integrated security permissions on a database.</p>
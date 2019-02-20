---
ID: 1430
post_title: >
  Microsoft SQL Server 2008 R2 setup
  starts, when you build a Visual Studio
  2010 setup project
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/05/26/microsoft-sql-server-2008-r2-setup-starts-when-you-build-a-visual-studio-2010-setup-project/
published: true
post_date: 2010-05-26 15:58:50
---
<p>When you build a Microsoft Visual Studio 2010 setup project a Microsoft SQL Server 2008 R2 setup might start. To solve this problem on a x64 system:</p>  <p><strong>regsvr32.exe /u &quot;C:\Program Files (x86)\Common Files\microsoft shared\MSI Tools\mergemod.dll&quot;     <br />regsvr32.exe &quot;C:\Program Files (x86)\Common Files\microsoft shared\MSI Tools\mergemod.dll&quot;</strong></p>  <p>on a x86 system</p>  <p><strong>regsvr32.exe /u &quot;C:\Program Files\Common Files\microsoft shared\MSI Tools\mergemod.dll&quot;     <br />regsvr32.exe &quot;C:\Program Files\Common Files\microsoft shared\MSI Tools\mergemod.dll&quot;</strong></p>
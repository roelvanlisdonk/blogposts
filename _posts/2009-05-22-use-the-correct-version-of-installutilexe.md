---
ID: 421
post_title: >
  Use the correct version of
  InstallUtil.exe
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/22/use-the-correct-version-of-installutilexe/
published: true
post_date: 2009-05-22 08:39:02
---
<p>When you want to use &quot;InstallUtil.exe&quot; for installing a windows service, make sure that you use the correct version. You can only uninstall a .NET 2.0 windows service with the &quot;InstallUtil.exe&quot; in the folder &quot;C:\WINDOWS\Microsoft.NET\Framework\v2.0.50727\InstallUtil.exe&quot;   <br />like:     <br />&quot;C:\WINDOWS\Microsoft.NET\Framework\v2.0.50727\InstallUtil.exe&quot; /u &quot;C:\Program Files\ADA ICT\WindowsService1.exe&quot;</p>
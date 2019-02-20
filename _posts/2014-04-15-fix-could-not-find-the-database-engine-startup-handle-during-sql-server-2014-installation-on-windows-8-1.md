---
ID: 3723
post_title: 'Fix: &lsquo;Could not find the Database Engine startup handle&rsquo; during SQL Server 2014 installation on Windows 8.1'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/04/15/fix-could-not-find-the-database-engine-startup-handle-during-sql-server-2014-installation-on-windows-8-1/
published: true
post_date: 2014-04-15 13:18:25
---
<p>After the installation of SQL Server 2014 was almost completed on a Windows 8.1 workstation, I got the error: &quot;Could not find the Database Engine startup handle&quot;.</p>  <p>&#160;</p>  <p>This was caused by the fact, that I used all standard settings during installation. When you choose all to install SQL Server 2014 with all default options, the SQL Server windows service will run under the NT Service\MSSQL$V2014 account, after changing this login to a correct login (a local admin account on the box) the service started correctly and I could login to the SQL Server 2014 instance.</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/04/image1.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/04/image_thumb1.png" width="580" height="21" /></a></p>
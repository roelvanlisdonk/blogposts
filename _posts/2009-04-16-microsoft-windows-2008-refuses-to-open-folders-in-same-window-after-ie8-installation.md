---
ID: 346
post_title: >
  Microsoft Windows 2008 refuses to open
  folders in same window after IE8
  installation
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/04/16/microsoft-windows-2008-refuses-to-open-folders-in-same-window-after-ie8-installation/
published: true
post_date: 2009-04-16 11:35:36
---
<p> After installing Microsoft IE 8 on Windows 2008, the Microsoft Windows Explorer refuses to open folders in the same window, even if the "Open each folder in the same window" is checked.<br /><br /><br /><a href="http://roelvanlisdonk.files.wordpress.com/2009/04/image.png"><img style="border-bottom:0;border-left:0;border-top:0;border-right:0;" border="0" alt="image" src="http://roelvanlisdonk.files.wordpress.com/2009/04/image-thumb.png" width="355" height="429"></a><br /><br /><br />Re-registering "actxprxy.dll" resolved this issue.  <p>&gt;Start &gt; Run &gt; regsvr32 actxprxy.dll<br />Log off an on, the settings should work again.</p>
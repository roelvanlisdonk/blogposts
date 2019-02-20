---
ID: 1994
post_title: >
  Identify the w3wp.exe process to attach
  Microsoft Visual Studio 2010 to
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/04/21/identify-the-w3wp-exe-process-to-attach-microsoft-visual-studio-2010-to/
published: true
post_date: 2011-04-21 09:28:02
---
<p>If you want to identify the w3wp.exe process to attach Microsoft Visual Studio 2010 you can use cscript for IIS6 en appcmd for IIS7:</p>  <p>&#160;</p>  <p><strong>IIS 6</strong></p>  <p>start &gt; cmd</p>  <p>%windir%\system32\cscript iisapp.vbs</p>  <p>&#160;</p>  <p><strong>IIS 7</strong></p>  <p>start &gt; cmd</p>  <p>%windir%\system32\inetsrv\appcmd.exe list wp</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/04/image4.png"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/04/image_thumb4.png" width="714" height="362" /></a></p>
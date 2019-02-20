---
ID: 3109
post_title: >
  How to enable JSON dynamic
  HttpCompression (gzip) on IIS in Windows
  8.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/12/13/how-to-enable-json-dynamic-httpcompression-gzip-on-iis-in-windows-8/
published: true
post_date: 2012-12-13 16:43:05
---
<p>First check if Dynamic compression is enabled:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/12/image56.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/12/image_thumb56.png" width="458" height="396" /></a></p>  <p>&#160;</p>  <p><strong>administration.config</strong></p>  <p>Open C:\Windows\System32\inetsrv\config\administration.config with notepad and change the httpCompression tag:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/12/image57.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/12/image_thumb57.png" width="580" height="294" /></a></p>  <p>&#160;</p>  <p>For IIS 7, also change the urlCompression tag:</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/12/image58.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/12/image_thumb58.png" width="580" height="23" /></a></p>  <p>&#160;</p>  <p><strong>ISA Server</strong></p>  <p>If the dynamic compression is still not working, verify there is no ISA server between the server and the client, if so follow the steps on <a title="http://forums.iis.net/t/1168067.aspx" href="http://forums.iis.net/t/1168067.aspx">http://forums.iis.net/t/1168067.aspx</a></p>  <p>To check if the ISA server is the problem just open a browser on the server en connect to the localhost url, check with fiddler if the dynamic compression works.</p>
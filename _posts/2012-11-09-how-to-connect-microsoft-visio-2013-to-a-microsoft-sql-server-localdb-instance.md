---
ID: 2939
post_title: >
  How to connect Microsoft Visio 2013 to a
  Microsoft SQL Server LocalDB instance
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/11/09/how-to-connect-microsoft-visio-2013-to-a-microsoft-sql-server-localdb-instance/
published: true
post_date: 2012-11-09 09:08:05
---
<p>If you connect Microsoft Visio 2013 to a Microsoft SQL Server LocalDb instance by using the standard (localdb)\V11.0 instance name, you might get the error: </p>  <p>[DBNETLIB][ConnectionOpen (Connect()).]SQL Server does not exist or access denied.</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/11/image3.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/11/image_thumb3.png" width="580" height="414" /></a></p>  <p>&#160;</p>  <p>To fix this error use the following instance name: np:\\.\pipe\LOCALDB#<strong>92FE49CE</strong>\tsql\query</p>  <p>The number in bold can be found in the Microsoft SQL Server Management Studio 2012 Server Properties dialog, when connected to the (localdb)\V11.0 instance:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/11/image4.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/11/image_thumb4.png" width="580" height="525" /></a></p>
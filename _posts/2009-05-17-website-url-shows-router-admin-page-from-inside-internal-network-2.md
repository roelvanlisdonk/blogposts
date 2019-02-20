---
ID: 404
post_title: >
  Website URL shows router admin page from
  inside internal network
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/17/website-url-shows-router-admin-page-from-inside-internal-network-2/
published: true
post_date: 2009-05-17 12:00:48
---
<p>If you have a domain like <a href="http://www.vanlisdonk.nl">http://www.vanlisdonk.nl</a> or <a href="http://www.roelvanlisdonk.nl">http://www.roelvanlisdonk.nl</a> and host these websites on you're own server. The websites will show the router admin page from inside you're network.     <br />Changing the windows host file in C:\Windows\System32\drivers\etc, routing the internal ip adres lets say 192.168.1.55 to <a href="http://www.vanlisdonk.nl">www.vanlisdonk.nl</a> solves the problem.     <br />    <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/05/image2.png"><img style="border-right-width: 0px; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/05/image-thumb2.png" width="915" height="141" /></a> </p>  <p>&#160;</p>  <p>The host file on all client pc's on you're internal network should look like this:    <br />    <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/05/image3.png"><img style="border-right-width: 0px; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/05/image-thumb3.png" width="476" height="201" /></a> </p>  <p>&#160;</p>  <p>See:    <br /><a title="http://www.howtoforge.com/forums/showthread.php?t=12475" href="http://www.howtoforge.com/forums/showthread.php?t=12475">http://www.howtoforge.com/forums/showthread.php?t=12475</a></p>
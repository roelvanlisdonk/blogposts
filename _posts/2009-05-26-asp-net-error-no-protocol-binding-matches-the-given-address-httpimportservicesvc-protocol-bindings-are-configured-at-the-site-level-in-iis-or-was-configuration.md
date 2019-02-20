---
ID: 504
post_title: 'ASP .NET error: No protocol binding matches the given address &#039;http://&#8230;./ImportService.svc&#039;. Protocol bindings are configured at the Site level in IIS or WAS configuration.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/26/asp-net-error-no-protocol-binding-matches-the-given-address-httpimportservicesvc-protocol-bindings-are-configured-at-the-site-level-in-iis-or-was-configuration/
published: true
post_date: 2009-05-26 13:47:56
---
<p>I got the asp .net error: No protocol binding matches the given address '<a href="http://..../ImportService.svc'">http://..../ImportService.svc'</a>. Protocol bindings are configured at the Site level in IIS or WAS configuration, because I did not do an iisreset after I changed the website binding (I added a hostheader).    <br />    <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/05/image12.png"><img style="border-bottom: 0px; border-left: 0px; border-top: 0px; border-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/05/image-thumb12.png" width="459" height="354" /></a></p>
---
ID: 1836
post_title: '&#8216;Sys&#8217; is undefined or ASP.NET Ajax client-side framework failed to load in a ASP .NET 4.0 website'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/11/18/sys-is-undefined-or-asp-net-ajax-client-side-framework-failed-to-load-in-a-asp-net-4-0-website/
published: true
post_date: 2010-11-18 16:42:12
---
<p align="left">I was getting the the error ['Sys' is undefined] and [ASP.NET Ajax client-side framework failed to load] in an ASP .NET 4.0 website. After reading and following the post [<a title="http://weblogs.asp.net/chrisri/archive/2007/02/02/demystifying-sys-is-undefined.aspx" href="http://weblogs.asp.net/chrisri/archive/2007/02/02/demystifying-sys-is-undefined.aspx">http://weblogs.asp.net/chrisri/archive/2007/02/02/demystifying-sys-is-undefined.aspx</a>] I found my solution.     <br />    <br />De ScriptResource.axd [long url] was throwing a 404 server error. This was caused by the fact that the website had an application pool set to .NET 4.0 but the [Handler Mappings] (see Screen dump 001) for the *.axd files where not registered. Even after executing the [aspnet_regiis –i –enable] the [Handler Mappings] where not registered. <strong>After re-creating the site, the error was resolved.</strong> The screen dump 002 shows the correct handler mappings.</p>  <p>&#160;</p>  <p><strong>Screen dump 001</strong></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/11/image14.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/11/image_thumb14.png" width="454" height="467" /></a> </p>  <p>&#160;</p>  <p><strong>Screen dump 002</strong></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/11/image15.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/11/image_thumb15.png" width="654" height="529" /></a></p>
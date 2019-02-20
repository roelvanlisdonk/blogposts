---
ID: 4386
post_title: >
  Filter SQL Server Profiler trace to only
  show queries send by specific machine /
  laptop
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/06/10/filter-sql-server-profiler-trace-to-only-show-queries-send-by-specific-machine-laptop/
published: true
post_date: 2015-06-10 11:23:28
---
<p>&#160;</p>  <p>If you want to filet the SQL Server Profiler trace, so only queries send from your laptop are captured, just filter on HostName:</p>  <p>&#160;</p>  <p><strong>First:</strong></p>  <p>Enable “Show all events”</p>  <p>Enable “Show all columns”</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/06/image1.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/06/image_thumb1.png" width="580" height="369" /></a></p>  <p>&#160;</p>  <p>Click on [Column Filters…]</p>  <p>“Select Column” [HostName]:</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/06/image2.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/06/image_thumb2.png" width="580" height="376" /></a></p>  <p>&#160;</p>  <p>Enter the name of the “laptop”:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/06/image3.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/06/image_thumb3.png" width="580" height="542" /></a></p>
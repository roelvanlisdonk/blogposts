---
ID: 1772
post_title: 'How to resolve: &quot;Unrecognized attribute &#8216;targetFramework&#8217;. Note that attribute names are case-sensitive&quot;'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/10/27/how-to-resolve-unrecognized-attribute-targetframework-note-that-attribute-names-are-case-sensitive/
published: true
post_date: 2010-10-27 13:55:49
---
<p>I was getting the error &quot;Unrecognized attribute 'targetFramework'. Note that attribute names are case-sensitive&quot; on an ASP .NET 4.0 website. This was caused by the application pool targeting the wrong .net framework, change the application pool to the correct .net framework and the error will be resolved.</p>  <p>&#160;</p>  <p><strong>Error</strong></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/10/image8.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/10/image_thumb8.png" width="758" height="381" /></a> </p>  <p><strong>Solution</strong></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/10/image9.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/10/image_thumb9.png" width="244" height="220" /></a></p>
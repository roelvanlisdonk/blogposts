---
ID: 4565
post_title: >
  Fingerprint bundles in path, not in
  query parameter with
  System.Web.Optimization and Visual
  Studio 2015
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/07/28/fingerprint-bundles-in-path-not-in-query-parameter-with-system-web-optimization-and-visual-studio-2015/
published: true
post_date: 2015-07-28 15:41:59
---
<p align="left">In my previous post (<a title="http://www.roelvanlisdonk.nl/?p=4550" href="http://www.roelvanlisdonk.nl/?p=4550">http://www.roelvanlisdonk.nl/?p=4550</a>) I explained how to:</p>  <p align="left">- create a new ASP .NET MVC 5 .NET 4.6 project in Visual Studio 2015</p>  <p align="left">- add static caching, add url rewrites</p>  <p align="left">- add fingerprinting to the “folder part” of each URL, to bust the client cache, when a new build is deployed to the website</p>  <p align="left">&#160;</p>  <p align="left">Now if you don’t want to use the URL Rewrite approach, but you still want to fingerprint the “folder url part” of the bundels created with the System.Web.Optimization (instead of using the standard query parameter cache busting technique), you can use the following class:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/07/image59.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/07/image_thumb59.png" width="580" height="426" /></a></p>  <p>&#160;</p>  <p>Use this class, when the bundles are created and when they are used inside the *.cshtml:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/07/image60.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/07/image_thumb60.png" width="580" height="378" /></a></p>  <p>&#160;</p>  <p>Then inside a *.cshtml page:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/07/image61.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/07/image_thumb61.png" width="580" height="191" /></a></p>  <p>&#160;</p>  <p>In this way, only the “name” of the bundle is fingerprinted and bundeling will only take place in “release” build.</p>  <p>The System.Web.Optimization will take care of the “cache busting”, no need for “URL rewriting”.</p>  <p>&#160;</p>  <p>The code uses the following extension method:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/07/image62.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/07/image_thumb62.png" width="580" height="278" /></a></p>
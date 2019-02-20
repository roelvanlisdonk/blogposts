---
ID: 4284
post_title: >
  UseWebApi not found / missing in Web API
  2.2
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/03/18/usewebapi-not-found-missing-in-web-api-2-2/
published: true
post_date: 2015-03-18 09:13:13
---
<p>If the IAppBuilder interface does not contain a “UseWebApi” function, this might be caused by a missing NuGetPackage “Microsoft.AspNet.WebApi.Owin”.   <br /></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/03/image.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/03/image_thumb.png" width="580" height="59" /></a></p>  <p>&#160;</p>  <p>After installing this NuGetPackage the function was available.</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/03/image1.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/03/image_thumb1.png" width="580" height="234" /></a></p>  <p>&#160;</p>  <p>&#160;</p>  <p>See: <a title="http://www.jeffwids.com/post/where-does-iappbuilderusewebapi-come-from" href="http://www.jeffwids.com/post/where-does-iappbuilderusewebapi-come-from">http://www.jeffwids.com/post/where-does-iappbuilderusewebapi-come-from</a></p>
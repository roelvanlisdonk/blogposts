---
ID: 4373
post_title: Fix favicon error
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/06/04/fix-favicon-error/
published: true
post_date: 2015-06-04 10:52:44
---
<p>When there is no favicon.ico in the root of your website, then the browser will automatically get a 404 favicon error.   <br />To prevent this error, you can add a transparent favicon.ico to the “head” tag of your HTML page:</p>  <p>&lt;link rel=&quot;icon&quot; href=&quot;data:;base64,iVBORw0KGgo=&quot;&gt;</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/06/image.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/06/image_thumb.png" width="567" height="248" /></a></p>
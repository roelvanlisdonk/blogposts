---
ID: 2201
post_title: 'Solving: CSC: Assembly generation &#8212; Referenced assembly &#8216;mscorlib.dll&#8217; targets a different processor in MSBUILD'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/11/10/solving-csc-assembly-generation-referenced-assembly-mscorlib-dll-targets-a-different-processor-in-msbuild/
published: true
post_date: 2011-11-10 16:52:18
---
<p>I was getting the warning / error in the MSBUILD output</p>  <p>CSC: Assembly generation -- Referenced assembly 'mscorlib.dll' targets a different processor in MSBUILD</p>  <p>&#160;</p>  <p>After setting the <strong>[MSBuild Platform]</strong> to <strong>[X86]</strong> in the build definition, the warnings / errors were resolved.</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/11/image3.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/11/image_thumb3.png" width="580" height="280" /></a></p>
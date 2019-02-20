---
ID: 1018
post_title: 'Warning: 0x7 at : Cannot debug script tasks when running under the 64 bit version of the Integration Services runtime in a SSIS package'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/02/10/warning-0x7-at-cannot-debug-script-tasks-when-running-under-the-64-bit-version-of-the-integration-services-runtime-in-a-ssis-package/
published: true
post_date: 2010-02-10 11:32:53
---
<p>If you get a warning like:</p>  <p>Warning: 0x7 at Filesysteem opschoning: Cannot debug script tasks when running under the 64 bit version of the Integration Services runtime.</p>  <p>when trying to debug a SSIS package, change the project property [Run64BitRuntime] to False:</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/02/image2.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/02/image_thumb2.png" width="510" height="315" /></a></p>
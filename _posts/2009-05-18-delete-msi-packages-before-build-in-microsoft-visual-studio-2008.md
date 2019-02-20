---
ID: 411
post_title: >
  Delete msi packages before build in
  Microsoft Visual Studio 2008
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/18/delete-msi-packages-before-build-in-microsoft-visual-studio-2008/
published: true
post_date: 2009-05-18 15:56:02
---
<p>Some times Microsoft Visual Studio 2008 will not re-create all *.msi packages when I rebuild all setup projects. Maybe this has something to do with source files not changing?   <br />To get around this problem, I just delete the *.msi pacakge before build with a Pre-Build event.    <br />    <br />Select you're setup project, press F4 to open properties window    <br />In the PreBuildEvent textbox enter:</p>  <p>cd &quot;$(TargetDir)&quot;   <br />del *.msi</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/05/image4.png"><img style="border-bottom: 0px; border-left: 0px; border-top: 0px; border-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/05/image-thumb4.png" width="354" height="268" /></a>     <br />    <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/05/image5.png"><img style="border-bottom: 0px; border-left: 0px; border-top: 0px; border-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/05/image-thumb5.png" width="244" height="137" /></a></p>
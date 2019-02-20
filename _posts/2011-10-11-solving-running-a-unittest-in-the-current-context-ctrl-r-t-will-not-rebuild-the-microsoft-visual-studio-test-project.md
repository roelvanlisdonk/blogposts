---
ID: 2167
post_title: 'Solving: Running a unittest in the current context [CTRL + R, T] will not rebuild the Microsoft Visual Studio Test project.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/10/11/solving-running-a-unittest-in-the-current-context-ctrl-r-t-will-not-rebuild-the-microsoft-visual-studio-test-project/
published: true
post_date: 2011-10-11 14:04:47
---
<p>Normally when you alter code in your Microsoft Visual Studio test project, pressing [CTRL + R, T] will rebuild the project and will execute the correct code. </p>  <p>In my case altering the code in the unit test did not result in recompiling the test project.</p>  <p>&#160;</p>  <p>Turns out the test project was disabled in the Configuration Manager:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/10/image2.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/10/image_thumb2.png" width="580" height="362" /></a></p>  <p>&#160;</p>  <p>Enabling the project in the configuration manager will resolve the problem.</p>
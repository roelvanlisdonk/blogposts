---
ID: 4258
post_title: 'How to fix: No gulp tasks found by the Task Runner Explorer in Visual Studio 2013'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/01/23/how-to-fix-no-gulp-tasks-found-by-the-task-runner-explorer-in-visual-studio-2013/
published: true
post_date: 2015-01-23 11:32:58
---
<p>The Task Runner Explorer extension for Microsoft Visual Studio 2013 found the gulpfile.js in my project, but the task in that file where not listed, just beneath the gulpfile.js, (No tasks found) was displayed, this was caused by missing dependencies.</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/01/image8.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/01/image_thumb8.png" width="201" height="160" /></a></p>  <p>&#160;</p>  <p>To fix this:</p>  <p>Just open a command prompt.</p>  <p>Change directory to the folder containing the file “gulpfile.js”</p>  <p>Then enter: npm install </p>  <p>All dependency for gulp should be installed, now when you op the project in Visual Studio 2013 the tasks should be shown.</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/01/image9.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/01/image_thumb9.png" width="233" height="244" /></a></p>
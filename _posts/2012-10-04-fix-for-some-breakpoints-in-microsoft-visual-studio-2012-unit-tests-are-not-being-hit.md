---
ID: 2846
post_title: 'Fix for: Some breakpoints in Microsoft Visual Studio 2012 unit tests are not being hit.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/10/04/fix-for-some-breakpoints-in-microsoft-visual-studio-2012-unit-tests-are-not-being-hit/
published: true
post_date: 2012-10-04 11:36:08
---
<p>When I opened a Microsoft Visual Studio 2010 solution in Microsoft Visual Studio 2012 and debugged my unit tests, some breakpoints where not hit and some code was stepped over, when using F11. </p>  <p>The problem was caused by the *.testsettings files in the solution folder after removing these files and restarting Microsoft Visual Studio 2012 the problem was fixed.</p>  <p>I found my solution at: </p>  <p><a href="http://social.msdn.microsoft.com/Forums/pl-PL/vsdebug/thread/ff6db2d5-42b4-42af-8d3b-a583cb7eaa96">http://social.msdn.microsoft.com/Forums/pl-PL/vsdebug/thread/ff6db2d5-42b4-42af-8d3b-a583cb7eaa96</a></p>
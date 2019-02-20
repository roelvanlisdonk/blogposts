---
ID: 3820
post_title: >
  Solving GitHub FetchHead (MergeConflict)
  in Visual Studio 2013
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/06/05/solving-github-fetchhead-mergeconflict-in-visual-studio-2013/
published: true
post_date: 2014-06-05 08:55:06
---
<p>I was getting the error:</p> An error occurred. Detailed message: An error was raised by libgit2. Category = FetchHead (MergeConflict).  <br />3 conflicts prevent checkout.  <p>&#160;</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/06/image2.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/06/image_thumb2.png" width="580" height="294" /></a></p>  <p>&#160;</p>  <p>To resolve this problem, I installed the 3rd-party Git command prompt tools, then you can open a Windows git command prompt from Visual Studio 2013: <a title="http://msdn.microsoft.com/en-us/library/vstudio/dd286572.aspx#commands" href="http://msdn.microsoft.com/en-us/library/vstudio/dd286572.aspx#commands">http://msdn.microsoft.com/en-us/library/vstudio/dd286572.aspx#commands</a></p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/06/image3.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/06/image_thumb3.png" width="566" height="325" /></a></p>  <p>&#160;</p>  <p>When I entered the command: git pull, I got the real error cause:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/06/image4.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/06/image_thumb4.png" width="580" height="93" /></a></p>  <p>&#160;</p>  <p>After removing these files and entering the commands:</p>  <p>git stash</p>  <p>git pull</p>  <p>The error was resolved.</p>
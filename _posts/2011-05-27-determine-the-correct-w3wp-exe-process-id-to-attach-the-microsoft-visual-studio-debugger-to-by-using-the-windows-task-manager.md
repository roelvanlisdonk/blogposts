---
ID: 2079
post_title: >
  Determine the correct w3wp.exe process
  ID, to attach the Microsoft Visual
  Studio debugger to, by using the Windows
  Task Manager
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/05/27/determine-the-correct-w3wp-exe-process-id-to-attach-the-microsoft-visual-studio-debugger-to-by-using-the-windows-task-manager/
published: true
post_date: 2011-05-27 11:42:25
---
<p>If you have multiple application pools started in IIS 7 and you want to determine which w3wp.exe process to attach the Microsoft Visual Studio 2010 debugger to, you can use the Microsoft Windows Task Manager.</p>  <p>Start the Microsoft Windows Task Manager: press [Ctrl + Shift + Esc].</p>  <p>Add the columns &quot;PID&quot; and &quot;Command Line&quot; to the Process tab.</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image23.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image_thumb23.png" width="580" height="314" /></a></p>  <p>&#160;</p>  <p>The name of the application pool will be shown in the Command Line Column.</p>  <p>In this case the WCF service I wanted to debug, was running on the default [ASP.NET v4.0] application pool. </p>  <p>The Microsoft Windows Task Manager, shows the PID of this w3wp.exe processes as 8188, so now I can attach the Microsoft Visual Studio debugger, to the process with ID 8188, to start debugging the WCF service</p>
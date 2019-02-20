---
ID: 1140
post_title: >
  Use VSCmdShell to run a PowerShell
  script from within Visual Studio 2008
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/18/use-vscmdshell-to-run-a-powershell-script-from-within-visual-studio-2008/
published: true
post_date: 2010-03-18 15:46:31
---
<p>You can use VSCmdShell to run a PowerShell script from within Visual Studio 2008.</p>  <p>After installing VSCmdShell you can change the startup folder (working folder) of the powershell window:</p>  <ul>   <li>Tools &gt; Options &gt; Power Toys &gt; VSCmdShell</li>    <li>Set Shell Selection: Windows PowerShell</li>    <li>Set Solution Root Directory as Starting Directory</li> </ul>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/03/image25.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/03/image_thumb25.png" width="804" height="467" /></a> </p>  <p>&#160;</p>  <p>To show the powershell command prompt in Visual Studio 2008 click View &gt; Shell Window (VSCmdShell)</p>  <p>To run a Test.ps1 PowerShell script, added to the Solution Items you can type .\Test.ps1</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/03/image26.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/03/image_thumb26.png" width="604" height="432" /></a></p>
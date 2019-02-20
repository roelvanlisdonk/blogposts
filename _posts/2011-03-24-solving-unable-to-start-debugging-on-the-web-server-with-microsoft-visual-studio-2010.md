---
ID: 1927
post_title: 'Solving: Unable to start debugging on the web server with Microsoft Visual Studio 2010'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/03/24/solving-unable-to-start-debugging-on-the-web-server-with-microsoft-visual-studio-2010/
published: true
post_date: 2011-03-24 19:54:17
---
<p>&#160;</p>  <p>I was getting the error &quot;Unable to start debugging on the web server. The remote debugging components are not registered or running on the web server. Ensure the proper version of msvsmon is running on the remote computer&quot;.</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/03/image2.png"><img style="background-image: none; border-right-width: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/03/image_thumb2.png" width="573" height="248" /></a></p>  <p align="left">&#160;</p>  <p align="left">In my case it was caused by 2 things.</p>  <p align="left">&#160;</p>  <p align="left"><strong>First</strong></p>  <p align="left">I installed the Microsoft Visual Studio 2010 Remote Debugger components from&#160; <a title="http://www.microsoft.com/downloads/details.aspx?FamilyID=60EC9D08-439B-4986-AE43-0487EB83C09E&amp;amp;displaylang=ja&amp;displaylang=en" href="http://www.microsoft.com/downloads/details.aspx?FamilyID=60EC9D08-439B-4986-AE43-0487EB83C09E&amp;amp;displaylang=ja&amp;displaylang=en">http://www.microsoft.com/downloads/details.aspx?FamilyID=60EC9D08-439B-4986-AE43-0487EB83C09E&amp;amp;displaylang=ja&amp;displaylang=en</a>, then completed the remote debugging configuration wizard, which will start automatically after installation of the Microsoft Visual Studio 2010 Remote Debugger components</p>  <p align="left">&#160;</p>  <p align="left"><strong>Secondly</strong></p>  <p align="left">The password of the identity of the application pool was changed</p>  <p align="left">After setting the correct password for the application pool identity in IIS and starting the application pool, the error was resolved. </p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/03/image3.png"><img style="background-image: none; border-right-width: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/03/image_thumb3.png" width="428" height="644" /></a></p>  <p>&#160;</p>  <p><strong>Note</strong></p>  <p>Make sure you’re application pool is running the correct .NET Version:</p>  <p>.NET 2.0, 3.0 and 3.5 web applications, should use an application pool that uses .NET 2.0</p>  <p>.NET 4.0 web application, should use an application pool that uses .NET 4.0</p>  <p>&#160;</p>  <p align="left">In some cases you might need to disable the loopback check in the registry in HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableLoopbackCheck (DWORD with value = 1).</p>
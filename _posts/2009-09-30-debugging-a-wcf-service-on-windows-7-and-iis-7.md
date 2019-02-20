---
ID: 722
post_title: >
  Debugging a WCF service on Windows 7 and
  IIS 7
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/09/30/debugging-a-wcf-service-on-windows-7-and-iis-7/
published: true
post_date: 2009-09-30 15:37:30
---
<p>I created and deployed a WCF service, created with Microsoft Visual Studio 2008, to IIS 7 on Windows 7 and I got the error message:   <br />Unable to start debugging on the web server. Could not start ASP .NET debugging. More Information may be available by starting the project without debugging.</p>  <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/09/image.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/09/image_thumb.png" width="500" height="226" /></a>   <br />  <br />  <p>So I did, I started the WCF service without debugging an got the error page:   <br />HTTP Error 404.3 - Not Found    <br />The page you are requesting cannot be served because of the extension configuration. If the page is a script, add a handler. If the file should be downloaded, add a MIME map.    <br />    <br />Then I followed the instruction on <a title="http://blogs.msdn.com/rjohri/archive/2009/06/29/the-page-you-are-requesting-cannot-be-served-because-of-the-extension-configuration.aspx" href="http://blogs.msdn.com/rjohri/archive/2009/06/29/the-page-you-are-requesting-cannot-be-served-because-of-the-extension-configuration.aspx">http://blogs.msdn.com/rjohri/archive/2009/06/29/the-page-you-are-requesting-cannot-be-served-because-of-the-extension-configuration.aspx</a>    <br />, that cleared the error!    <br /></p>  <li>Run Visual Studio 2008 Command Prompt as “Administrator”. </li>  <li>Navigate to C:\Windows\Microsoft.NET\Framework\v3.0\Windows Communication Foundation. </li>  <li>Run this command servicemodelreg –i</li>  <p>&#160;</p>  <p>Installed IIS 7 after installing Visual Studio 2008 and .NET Framework 3.5</p>
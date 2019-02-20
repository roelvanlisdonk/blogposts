---
ID: 2081
post_title: 'Solving: Could not load file or assembly &#8216;App_Web_squ1ikqu, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null&#8217; or one of its dependencies. The system cannot find the file specified in .NET 4.0'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/06/01/solving-could-not-load-file-or-assembly-app_web_squ1ikqu-version0-0-0-0-cultureneutral-publickeytokennull-or-one-of-its-dependencies-the-system-cannot-find-the-file-specified-in-net-4-0/
published: true
post_date: 2011-06-01 08:32:55
---
<p>After we virtualized a production machine and booted this virtualized machine, .NET reported some errors after re-registering .NET 4.0 on IIS7 these error where resolved, but one WCF service kept on logging the error:</p>  <p><strong>Could not load file or assembly 'App_Web_squ1ikqu, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null' or one of its dependencies. The system cannot find the file specified.</strong></p>  <p>&#160;</p>  <p><strong>Solution</strong></p>  <p>The error was resolved after stopping all application pools in IIS7 and deleting the temporary internet files in the following folders:</p>  <ul>   <li>C:\Windows\Microsoft.NET\Framework\v2.0.50727\Temporary ASP.NET Files</li>    <li>C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files</li>    <li>C:\Windows\Microsoft.NET\Framework64\v2.0.50727\Temporary ASP.NET Files</li>    <li>C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Temporary ASP.NET Files</li> </ul>
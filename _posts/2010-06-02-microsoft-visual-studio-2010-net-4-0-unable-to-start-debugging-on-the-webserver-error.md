---
ID: 1436
post_title: 'Microsoft Visual Studio 2010 .NET 4.0 &ldquo;Unable to start debugging on the webserver&rdquo; error'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/06/02/microsoft-visual-studio-2010-net-4-0-unable-to-start-debugging-on-the-webserver-error/
published: true
post_date: 2010-06-02 11:31:45
---
<p>I could debug web applications in Microsoft Visual Studio 2010, when the target framework was .NET 3.5, but when changed to .NET 4.0 I got the error: Unable to start debugging on the webserver.</p>  <p><strong>Solution</strong></p>  <p>Run “C:\Windows\Microsoft.NET\Framework\v4.0.30319&gt;aspnet_regiis.exe -i”</p>
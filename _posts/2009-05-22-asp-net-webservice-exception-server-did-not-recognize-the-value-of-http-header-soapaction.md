---
ID: 458
post_title: 'ASP .NET webservice exception: Server did not recognize the value of HTTP Header SOAPAction'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/22/asp-net-webservice-exception-server-did-not-recognize-the-value-of-http-header-soapaction/
published: true
post_date: 2009-05-22 15:19:21
---
<p>When you get the error &#8220;Server did not recognize the value of HTTP Header SOAPAction&#8221;    <br />1. Check if the website uses the correct version of the .NET Framework. Use aspnet_regiis &#8211;i to install the correct version of the .NET Framework on your IIS website.     <br />2. Check if the ASP .NET v2.0.50727 pages are allowed:     <br />3. Renew / update your webreference and rebuild your project in Microsoft Visual Studio</p>
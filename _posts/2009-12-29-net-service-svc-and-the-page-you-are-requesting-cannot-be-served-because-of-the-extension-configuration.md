---
ID: 892
post_title: '.NET service (.svc) and &#8220;The page you are requesting cannot be served because of the extension configuration&#8221;'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/12/29/net-service-svc-and-the-page-you-are-requesting-cannot-be-served-because-of-the-extension-configuration/
published: true
post_date: 2009-12-29 08:39:55
---
<p>When you want to debug a .net service (*.svc) and you get the error: “The page you are requesting cannot be served because of the extension configuration”.   <br />    <br />Try the solution on: <a title="http://tonytriguero.com/iis-7-and-webservices-svc-file-extension/" href="http://tonytriguero.com/iis-7-and-webservices-svc-file-extension/">http://tonytriguero.com/iis-7-and-webservices-svc-file-extension/</a></p>  <li>Open Visual Studio 2008 Command prompt. </li>  <li>Navigate to C:\Windows\Microsoft.NET\Framework\v3.0\Windows Communication Foundation</li>  <li>Run this command: servicemodelreg –i</li>
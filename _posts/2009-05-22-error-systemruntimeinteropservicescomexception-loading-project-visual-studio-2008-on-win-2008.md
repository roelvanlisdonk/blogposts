---
ID: 460
post_title: >
  Error
  System.Runtime.InteropServices.COMException
  loading project Visual Studio 2008 on
  Win 2008
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/22/error-systemruntimeinteropservicescomexception-loading-project-visual-studio-2008-on-win-2008/
published: true
post_date: 2009-05-22 15:26:16
---
<p>After reinstalling windows 2008 en visual studio 2008, i got an error when loading an ASP .NET website en webservice project. Installing the IIS 6 Management Compatibility and creating the correct virtual directories resolved the error.</p>  <p>For the correct virtual directories, open the .csproj en find the xml tag:</p>  <p>&lt;IISUrl&gt;<a href="http://&hellip;...local/TestWeb">http://&#8230;...local/TestWeb</a>&lt;/IISUrl&gt;     <br />This virtual directory must exist.</p>
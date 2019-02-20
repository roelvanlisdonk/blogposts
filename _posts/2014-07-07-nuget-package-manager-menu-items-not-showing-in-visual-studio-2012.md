---
ID: 3930
post_title: >
  NuGet Package Manager menu items not
  showing in Visual Studio 2012.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/07/07/nuget-package-manager-menu-items-not-showing-in-visual-studio-2012/
published: true
post_date: 2014-07-07 15:24:24
---
<p>I had installed Visual Studio 2010 and Visual Studio 2012 and installed the NuGet Package Manager, via [Extensions and Updates] and no NuGet Package Manager was showing.</p>  <p>I found the solution add: <a title="http://nuget.codeplex.com/workitem/3031" href="http://nuget.codeplex.com/workitem/3031">http://nuget.codeplex.com/workitem/3031</a></p>  <p>&#160;</p>  <p>Manual downloading the NuGet Package Manager (vsix), closing all visual studio instances and running the *.vsix twice simultaneous, fixed the problem.</p>
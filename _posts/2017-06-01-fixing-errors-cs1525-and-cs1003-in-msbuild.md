---
ID: 5075
post_title: >
  Fixing errors CS1525 and CS1003 in
  MSBuild
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2017/06/01/fixing-errors-cs1525-and-cs1003-in-msbuild/
published: true
post_date: 2017-06-01 11:00:11
---
<p>When building a Microsoft Visual Studio 2017 solution that uses C#6 and C#7 features from the command line (PowerShell), I was getting the errors:</p>    <p>MyClass.cs(845,112): error CS1525: Invalid expression term 'decimal' [Web.csproj]   <br />MyClass.cs(845,120): error CS1003: Syntax error, ',' expected [Web.csproj]    <br />MyClass.cs(870,116): error CS1525: Invalid expression term 'decimal' [Web.csproj]    <br />MyClass.cs(870,124): error CS1003: Syntax error, ',' expected [Web.csproj]</p>    <p>This was caused by using the wrong version of MSBuild.</p>  <p>I used &quot;C:\Program Files (x86)\MSBuild\14.0\Bin\MSBuild.exe&quot; after switching to</p>  <p>&quot;C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\MSBuild\15.0\Bin\MSBuild.exe&quot;<strong> </strong>the problem was resolved.</p>
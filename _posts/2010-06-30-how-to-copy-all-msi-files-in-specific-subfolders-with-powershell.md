---
ID: 1576
post_title: 'How to copy all *.msi files from specific subfolders with PowerShell'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/06/30/how-to-copy-all-msi-files-in-specific-subfolders-with-powershell/
published: true
post_date: 2010-06-30 14:10:39
---
<p>If you have a Microsoft Visual Studio 2010 solution, which contains setup projects and you want to copy all msi packages from the “Release” folders to one folder you can use the following script:</p>  <p>&#160;</p>  <p>$SourceFolder = &quot;C:\Source&quot;   <br />$DestinationFolder = &quot;C:\Destination&quot; </p>  <p>&quot;Copy *.msi packages from [Release] subfolders in $SourceFolder to the $DestinationFolder&quot;   <br />if(Test-Path $SourceFolder )    <br />{    <br />&#160;&#160;&#160; foreach ($item in Get-ChildItem &quot;$SourceFolder&quot; -filter &quot;*.msi&quot; -recurse)    <br />&#160;&#160;&#160; {    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; if ($item.FullName -like &quot;*Release*&quot; )    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; {    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; Copy-Item $item.FullName -Destination &quot;$DestinationFolder&quot;    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; }    <br />&#160;&#160;&#160; }     <br />}</p>
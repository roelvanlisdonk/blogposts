---
ID: 1142
post_title: >
  How to determine the program files
  folder with PowerShell, by using enums
  and nested types
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/19/how-to-determine-the-program-files-folder-with-powershell-by-using-enums-and-nested-types/
published: true
post_date: 2010-03-19 14:01:55
---
<p>If you want to use the systems “%PROGRAMFILES%” folder in PowerShell, use:</p>  <p>&#160;</p>  <p>$rootInstallationFolder = [System.Environment]::GetFolderPath([System.Environment+SpecialFolder]::ProgramFiles)   <br />$rootInstallationFolder</p>  <p><strong>Result</strong></p>  <p>C:\Program Files (x86)   <br /></p>  <p><strong>Note</strong></p>  <p>Because SpecialFolders is a nested type in System.Environment, you must use the “+” sign and not a “.”, else you get the error:</p>  <p>Unable to find type [System.Environment.SpecialFolder]: make sure that the assembly containing this type is loaded.</p>
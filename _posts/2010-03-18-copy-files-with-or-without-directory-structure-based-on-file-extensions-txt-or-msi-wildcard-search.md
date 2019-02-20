---
ID: 1133
post_title: 'Copy files with or without directory structure based on file extensions (*.txt or *.msi) wildcard search in PowerShell'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/18/copy-files-with-or-without-directory-structure-based-on-file-extensions-txt-or-msi-wildcard-search/
published: true
post_date: 2010-03-18 11:56:08
---
<p>If you want to copy all *.txt files in folder C:\Source to C:\Destination <strong><font color="#0000ff">preserving</font></strong> the directory structure:</p>  <p>&#160;</p>  <p><strong>Source files</strong></p>  <p>C:\Source\Test1.cmd</p>  <p>C:\Source\Test1.txt</p>  <p>C:\Source\Dir1\Test2.txt</p>  <p>&#160;</p>  <p><strong>PowerShell statement</strong></p>  <p>Copy-Item &quot;C:\Source&quot; &quot;C:\Destination&quot; -filter &quot;*.txt&quot; -recurse –force</p>  <p>&#160;</p>  <p><strong>Result (directory structure is preserved)</strong></p>  <p>C:\Destination\Source\Test1.txt</p>  <p>C:\Destination\Source\Dir1\Test2.txt</p>  <p>&#160;</p>  <p>&#160;</p>  <p>If you want to copy all *.txt files in folder C:\Source to C:\Destination <strong><font color="#0000ff">without preserving</font></strong> the directory structure:</p>  <p>&#160;</p>  <p><strong>Source files</strong></p>  <p>C:\Source\Test1.cmd</p>  <p>C:\Source\Test1.txt</p>  <p>C:\Source\Dir1\Test2.txt</p>  <p>&#160;</p>  <p><strong>PowerShell statement</strong></p>  <p>Get-ChildItem &quot;C:\Source&quot; -recurse -force -filter &quot;*.txt&quot; | Copy-Item -Destination &quot;C:\Destination&quot;</p>  <p>&#160;</p>  <p><strong>Result (directory structure is&#160; not preserved)</strong></p>  <p>C:\Destination\Test1.txt</p>  <p>C:\Destination\Test2.txt</p>
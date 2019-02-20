---
ID: 1860
post_title: 'Using C# in PowerShell to move files'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/12/29/using-c-in-powershell-to-move-files/
published: true
post_date: 2010-12-29 11:17:01
---
<p>&#160;</p>  <h2>Screedump form Windows PowerShell ISE</h2>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/12/image3.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/12/image_thumb3.png" width="704" height="415" /></a> </p>  <p>&#160;</p>  <h2>Code</h2>  <p>$source = @&quot; </p>  <p>using System;   <br />using System.Collections.Generic;    <br />using System.Text;    <br />using System.IO; </p>  <p>namespace Rvl.Demo.Common   <br />{    <br />&#160;&#160;&#160; public class MoveFiles    <br />&#160;&#160;&#160; {    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; public static void Move()    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; {    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; string sourceFolder = @&quot;C:\BDATA\Test\Source&quot;; // Source folder    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; string destinationFolder = @&quot;C:\BDATA\Test\Destination&quot;; // Destination folder    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; DateTime checkDateTime = new DateTime(2010, 12, 29, 13, 0, 0); // 27-dec-2010 13:00:00    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; // Loop all files in source folder    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; foreach (string file in Directory.GetFiles(sourceFolder))    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; {    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; // Calculate difference between checkDateTime and file last modified datetime in days    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; DateTime fileLastModifiedDate = File.GetLastWriteTime(file);</p>  <p>&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; // Move files if difference in days == 0   <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; if (checkDateTime.Year == fileLastModifiedDate.Year &amp;&amp; checkDateTime.Month == fileLastModifiedDate.Month &amp;&amp; checkDateTime.Day == fileLastModifiedDate.Day)    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; {    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; string destinationFilePath = Path.Combine(destinationFolder, Path.GetFileName(file));    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; Console.WriteLine(string.Format(&quot;Moving file [{0}] to [{1}]&quot;, file, destinationFilePath)); </p>  <p>&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; File.Move(file, destinationFilePath);   <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; }    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; }    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; }    <br />&#160;&#160;&#160; }    <br />}    <br />&quot;@ </p>  <p>Add-Type -TypeDefinition $source </p>  <p>[Rvl.Demo.Common.MoveFiles]::Move() </p>
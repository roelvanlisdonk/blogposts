---
ID: 1157
post_title: '# How to list members of the local computer group [IIS_IUSRS] with PowerShell'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/26/how-to-list-members-of-the-local-computer-group-iis_iusrs-with-powershell/
published: true
post_date: 2010-03-26 14:01:07
---
<p>If you want to list all members of the local computer group IIS_IUSRS with PowerShell, use this script:</p>  <p>&#160;</p>  <p><strong>[Script]</strong></p>  <p>&quot;Set execution policy to [Unrestricted]&quot;    <br />Set-ExecutionPolicy Unrestricted </p>  <p>$iisIUSRS = [ADSI]&quot;WinNT://L014/IIS_IUSRS,group&quot; </p>  <p>&quot;Loop members&quot;   <br />foreach ($member in $iisIUSRS.Invoke(&quot;Members&quot;, $null))    <br />{    <br />&#160;&#160;&#160; # Cast object to type DirectoryEntry    <br />&#160;&#160;&#160; $de = New-Object System.DirectoryServices.DirectoryEntry($member)    <br />&#160;&#160;&#160; # Determine username    <br />&#160;&#160;&#160; $userName = $de.Name    <br />&#160;&#160;&#160; # Show the username    <br />&#160;&#160;&#160; &quot;Member is $userName&quot;    <br />}</p>  <p>&#160;</p>  <p><strong>[Result]</strong></p>  <p>PS C:\Temp&gt; C:\Temp\Test.ps1   <br />Set execution policy to [Unrestricted]    <br />Loop members    <br />Member is SQLServerReportServerUser$L001$MSRS10.MSSQLSERVER    <br />Member is Administrator    <br />Member is saAsaWeb</p>
---
ID: 1135
post_title: 'How to install and un-install *.msi package with PowerShell and msiexec'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/18/how-to-install-and-un-install-msi-package-with-powershell-and-msiexec/
published: true
post_date: 2010-03-18 14:25:15
---
<p>If you want to install a *.msi package by first un-installing the product and then installing, you can use the following PowerShell script:</p>  <p>Use System.Diagnostics.Process.Start function and the WaitForExit function to make sure the product is un-installed before it is installed.</p>  <p>&#160;</p>  <p># This scripts needs unrestricted access   <br />Set-ExecutionPolicy Unrestricted </p>  <p># Change working directory to script directory   <br />function Get-ScriptDirectory    <br />{    <br />&#160;&#160;&#160; $Invocation = (Get-Variable MyInvocation -Scope 1).Value    <br />&#160;&#160;&#160; Split-Path $Invocation.MyCommand.Path    <br />}    <br />$scriptFolder = Get-ScriptDirectory </p>  <p># Un-Install Database   <br />$parameters = &quot;/qn /x {B381D4FB-7A5C-4794-8997-8CAAF2847E20}&quot;    <br />$uninstallStatement = [System.Diagnostics.Process]::Start( &quot;msiexec&quot;, $parameters )     <br />$uninstallStatement.WaitForExit()    <br /># Install Database    <br />$parameters = &quot;/qn /i &quot; + $scriptFolder + &quot;\Sales.Database.Setup.msi&quot;    <br />$installStatement = [System.Diagnostics.Process]::Start( &quot;msiexec&quot;, $parameters )     <br />$installStatement.WaitForExit()</p>
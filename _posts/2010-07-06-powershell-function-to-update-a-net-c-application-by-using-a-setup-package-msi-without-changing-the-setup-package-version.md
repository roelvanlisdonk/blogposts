---
ID: 1589
post_title: 'PowerShell function to update a .net C# application, by using a setup package (*.msi), without changing the setup package version'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/07/06/powershell-function-to-update-a-net-c-application-by-using-a-setup-package-msi-without-changing-the-setup-package-version/
published: true
post_date: 2010-07-06 16:56:48
---
<p>The output of a Microsoft Visual Studio Setup Project is a setup package (*.msi). If you run this setup package on a system, you can’t re-install the package on that system, without changing the version of the setup package. If you want to update the .net C# application without changing the version number, you can use the following PowerShell script:</p>  <p>&#160;</p>  <p>function DeploySubsystem([string]$name, [string]$msiPackageProductCodeGuid, [string]$msiPackagePath)   <br />{    <br />&#160;&#160;&#160; &quot;Uninstall $name&quot;    <br />&#160;&#160;&#160; $parameters = &quot;/qn /x $msiPackageProductCodeGuid&quot;    <br />&#160;&#160;&#160; $processPath = &quot;msiexec&quot;    <br />&#160;&#160;&#160; &quot;Run [$processPath $parameters]&quot;    <br />&#160;&#160;&#160; $process = [System.Diagnostics.Process]::Start( $processPath, $parameters )     <br />&#160;&#160;&#160; $process.WaitForExit() </p>  <p>&#160;&#160;&#160; &quot;Sleep for 5 seconds to make sure the system has updated the registry&quot;   <br />&#160;&#160;&#160; [System.Threading.Thread]::Sleep(5000) </p>  <p>&#160;&#160;&#160; &quot;Install $name&quot;   <br />&#160;&#160;&#160; $parameters = &quot;/qn /i &quot;&quot;$msiPackagePath&quot;&quot;&quot;    <br />&#160;&#160;&#160; $processPath = &quot;msiexec&quot;    <br />&#160;&#160;&#160; &quot;Run [$processPath $parameters]&quot;    <br />&#160;&#160;&#160; $process = [System.Diagnostics.Process]::Start( $processPath, $parameters )     <br />&#160;&#160;&#160; $process.WaitForExit()    <br />}</p>  <p></p>  <p>&#160;</p>  <p align="left">To call the function use:</p>  <p align="left">DeploySubsystem &quot;MyFirstApplicaiton&quot; &quot;{396E89DB-5E5C-4781-9E88-0FEC56D9C06C}&quot; &quot;C:\Temp\MyFirstApplication.Setup.msi&quot;&#160;&#160;&#160; </p>
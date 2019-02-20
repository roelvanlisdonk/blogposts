---
ID: 4973
post_title: >
  How to create an IIS application pool
  and web site on Windows 10 with
  PowerShell and Visual Studio Code
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2016/08/18/how-to-create-an-iis-application-pool-and-web-site-on-windows-10-with-powershell-and-visual-studio-code/
published: true
post_date: 2016-08-18 07:39:25
---
<p>Tasks to create an IIS application pool and web site on Windows 10 with PowerShell and Visual Studio Code:</p>  <ul>   <li>Install the Visual Studio Code plugin PowerShell 0.6.2</li>    <li>Create a file iis.configuration.ps1 in Visual Studio Code:</li> </ul>  <ul></ul>  <pre><p># Note: When run with the Visual Studio Code PowerShell debugger, make sure you use the &quot;x64&quot; debugger,   <br />#&#160;&#160;&#160;&#160;&#160;&#160; else you will get an error: New-WebAppPool : Cannot retrieve the dynamic parameters for the cmdlet.</p>
<p>Import-Module WebAdministration</p><p>
</p><p># Create application pools <br />New-WebAppPool -Name &quot;myapp.localhost&quot; -Force

</p><p># Create websites  <br />New-Website -Name &quot;myapp.localhost&quot; -Port 80 -HostHeader &quot;myapp.localhost&quot; -ApplicationPool &quot;myapp.localhost&quot; -PhysicalPath &quot;c:\projects\myapp\web&quot; -Force</p></pre>

<ul></ul>

<ul></ul>



<ul>
  <li>Create a launch.json in the same folder as the iis.configuration.ps1:</li>
</ul>



<ul></ul>

<pre><p>{   <br />&#160;&#160;&#160; &quot;version&quot;: &quot;0.2.0&quot;,   <br />&#160;&#160;&#160;&#160; &quot;configurations&quot;: [  <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; {   <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &quot;name&quot;: &quot;PowerShell&quot;,   <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &quot;type&quot;: &quot;PowerShell&quot;,   <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &quot;request&quot;: &quot;launch&quot;,   <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &quot;program&quot;: &quot;${workspaceRoot}/iis.configuration.ps1&quot;,   <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &quot;args&quot;: [],   <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &quot;cwd&quot;: &quot;${workspaceRoot}/iis.configuration.ps1&quot;   <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; },   <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; {   <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &quot;name&quot;: &quot;PowerShell x86&quot;,   <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &quot;type&quot;: &quot;PowerShell x86&quot;,   <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &quot;request&quot;: &quot;launch&quot;,   <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &quot;program&quot;: &quot;${workspaceRoot}/iis.configuration.ps1&quot;,   <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &quot;args&quot;: [],   <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &quot;cwd&quot;: &quot;${workspaceRoot}/iis.configuration.ps1&quot;   <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; }   <br />&#160;&#160;&#160; ]   <br /> }</p></pre>



<p>Now you can debug / run the iis.configuration.ps1 file, by hitting F5, make sure you selected “PowerShell” and not “PowerShell x86” on the debug tab:</p>



<p><a href="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/08/image.png" rel="lightbox"><img title="image" style="display: inline; background-image: none;" border="0" alt="image" src="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/08/image_thumb.png" width="279" height="451" /></a></p>
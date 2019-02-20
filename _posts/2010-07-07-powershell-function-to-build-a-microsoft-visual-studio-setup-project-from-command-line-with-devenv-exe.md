---
ID: 1591
post_title: >
  PowerShell function to build a Microsoft
  Visual Studio setup project from command
  line with devenv.exe
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/07/07/powershell-function-to-build-a-microsoft-visual-studio-setup-project-from-command-line-with-devenv-exe/
published: true
post_date: 2010-07-07 09:14:47
---
<p>If you want to build you’re Microsoft Visual Studio 2010 setup project in release mode, from the command line, you can use the following PowerShell function:   <br />    <br /></p>  <p>function RebuildSubsystem([string]$solutionPath, [string]$projectPath, [string]$devEnvPath)   <br />{    <br />&#160;&#160;&#160; $parameters = &quot;/Rebuild Release &quot;&quot;$solutionPath&quot;&quot; /Project &quot;&quot;$projectPath&quot;&quot; /ProjectConfig Release&quot;    <br />&#160;&#160;&#160; &quot;Process to start [$devEnvPath $parameters]&quot;     <br />&#160;&#160;&#160; $process = [System.Diagnostics.Process]::Start( &quot;$devEnvPath&quot;, $parameters )     <br />&#160;&#160;&#160; $process.WaitForExit()    <br />}</p>  <p>&#160;</p>  <p>To call the function use:</p>  <p align="left">RebuildSubsystem &quot;C:\Projects\MyApplication\MyApplication.sln&quot; &quot;C:\Projects\MyApplication\MyApplication.Setup\MyApplication.Setup.vdproj&quot; &quot;C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\devenv.exe&quot;   </p>
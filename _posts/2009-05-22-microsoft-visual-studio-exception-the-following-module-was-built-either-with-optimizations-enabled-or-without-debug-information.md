---
ID: 437
post_title: 'Microsoft Visual Studio exception: The following module was built either with optimizations enabled or without debug information'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/22/microsoft-visual-studio-exception-the-following-module-was-built-either-with-optimizations-enabled-or-without-debug-information/
published: true
post_date: 2009-05-22 13:20:20
---
<p>When debugging a GAC deployed assembly in Microsoft Visual Studio .NET 2005 with TestDriven .NET and NUnit, i get the error:</p>  <p><strong>The following module was built either with optimizations enabled or without debug information: C:\WINDOWS\assembly\GAC_MSIL\.....</strong></p>  <p><strong>To debug this module, change its project build configuration to Debug mode. To suppress this message, disable the &quot;Warn if no user code on launch&quot; debugger option</strong>.</p>  <p>This exception is caused by the fact, that the assembly was deployed to the GAC. If you want to debug this assembly. Remove the dll from the GAC (C:\WINDOWS\assembly) directory and make sure the assembly is referenced by the UnitTest project in Microsoft Visual Studio 2005 and Copy local is set to true.</p>  <p>After rebuilding the UnitTest project with debug configuration. The \bin\Debug directory should contain the dll to debug en the *.pdb file of that assembly.</p>  <p>Make sure all project are build with the following properties:</p>  <p>&lt;DebugSymbols&gt;true&lt;/DebugSymbols&gt;    <br />&lt;DebugType&gt;full&lt;/DebugType&gt;     <br />&lt;Optimize&gt;false&lt;/Optimize&gt;     <br />&lt;OutputPath&gt;bin\Debug\&lt;/OutputPath&gt;     <br />&lt;DefineConstants&gt;DEBUG;TRACE&lt;/DefineConstants&gt;</p>
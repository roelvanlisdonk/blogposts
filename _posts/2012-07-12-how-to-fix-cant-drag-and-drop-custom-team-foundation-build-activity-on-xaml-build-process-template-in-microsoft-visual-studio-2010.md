---
ID: 2769
post_title: 'How to fix: Can&#8217;t drag and drop custom Team Foundation Build Activity on XAML build process template in Microsoft Visual Studio 2010.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/07/12/how-to-fix-cant-drag-and-drop-custom-team-foundation-build-activity-on-xaml-build-process-template-in-microsoft-visual-studio-2010/
published: true
post_date: 2012-07-12 15:29:58
---
<p align="left">A .NET 4.0 assembly containing a custom Team Foundation Build Activity can only be dragged and dropped from the toolbox on your build process template XAML file, when it is first registered in the GAC. For registering a .NET 4.0 assembly in the GAC you will have to use the gacutil.exe for .NET 4.0 found at [C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\Bin\<strong>NETFX 4.0 Tools</strong>\gacutil.exe].</p>  <p align="left">If you don’t register the assemlby in the GAC you can’t drag and drop the Team Foundation Build Activity on the build process template XAML file. If it was added by an other developer, you get the error: &quot;<strong>Activity could not be loaded because of errors in the XAML</strong>&quot;:</p>  <p align="left">&#160;</p>  <p align="left"><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/07/image2.png" rel="lightbox"><img style="background-image: none; border-right-width: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/07/image_thumb2.png" width="580" height="491" /></a></p>  <p align="left">&#160;</p>  <p align="left">&#160;</p>  <p align="left">After registering the .NET 4. 0 assembly with the gacutil.exe, the assembly can be found at [C:\Windows\Microsoft.NET\assembly\GAC_MSIL].</p>  <p align="left">After registering, make sure you restart Microsoft Visual Studio 2010 before you drag and drop the custom Team Foundation Build Activity on your build process template XAML file.</p>
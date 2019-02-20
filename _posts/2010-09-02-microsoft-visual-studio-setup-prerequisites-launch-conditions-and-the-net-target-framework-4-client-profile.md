---
ID: 1715
post_title: >
  Microsoft Visual Studio Setup
  prerequisites, launch conditions and the
  .NET Target Framework 4 Client Profile
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/09/02/microsoft-visual-studio-setup-prerequisites-launch-conditions-and-the-net-target-framework-4-client-profile/
published: true
post_date: 2010-09-02 15:05:08
---
<p>When I changed the prerequisites for my Microsoft Visual Studio setup project to target the .NET Framework 4 and not the .NET Framework 4 Client Profile, I got the message:</p>  <p><strong>The target version of the .NET Framework in the project does not match the .NET Framework launch condition version '.NET Framework 4 Client Profile'. Update the version of the .NET Framework launch condition to match the target version of the.NET Framework in the Advanced Compile Options Dialog Box (VB) or the Application Page (C#, F#).</strong></p>  <p>&#160;</p>  <p>This was caused by the fact, that the setup Launch condition was still on Microsoft .NET Framework 4 Client Profile</p>  <p>&#160;</p>  <p><strong>Solution</strong></p>  <p>Change the Setup Launch condition to match you’re setup prerequisites:</p>  <ul>   <li>Select you’re project in the Solution Explorer</li>    <li>Click on the Launch Conditions Editor button</li> </ul>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/09/image.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/09/image_thumb.png" width="504" height="127" /></a> </p>  <p>&#160;</p>  <p><strong>Note 1</strong></p>  <p>You can change the prerequisites of you’re Microsoft Visual Studio setup project, by right clicking on the setup project, choose properties and click on Prerequisites…</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/09/image1.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/09/image_thumb1.png" width="504" height="360" /></a> </p>  <p>Change to Microsoft .NET Framework 4 and not Microsoft .NET Framework 4 Client Profile:</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/09/image2.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/09/image_thumb2.png" width="504" height="392" /></a> </p>  <p>&#160;</p>  <p><strong>Note 2</strong></p>  <p>When you are working with Microsoft Visual Studio setup projects make sure the following settings are in sync:</p>  <p>- Project Target framework for the projects the setup references</p>  <p>- Prerequisites of the setup project</p>  <p>- Launch condition of the setup project</p>
---
ID: 264
post_title: >
  Silent update for an application
  deployed with a Microsoft Visual Studio
  Setup Package
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/03/06/silent-update-for-an-application-deployed-with-a-microsoft-visual-studio-setup-package/
published: true
post_date: 2009-03-06 10:54:38
---
<p>If you have an application deployed with a Microsoft Visual Studio Setup Package, you can update you're application with a bat file containing:<br /><br /></p> <p>msiexec /qn /x {F447D60D-3582-4AF9-9D59-6B0A82F8E3C5}<br />msiexec /qn /i "C\Temp\TestProgram1.Setup.msi"
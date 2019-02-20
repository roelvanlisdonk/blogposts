---
ID: 2001
post_title: 'Solving Windows 7 can&rsquo;t boot on Vertex 3 on a DELL XPS L702.x'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/05/05/solving-windows-7-cant-boot-on-vertex-3-on-a-dell-xps-l702-x/
published: true
post_date: 2011-05-05 11:06:31
---
<p align="left">The BIOS of my Dell XPS L702.x was set to AHCI modus. Installing Windows 7 failed.</p>  <p align="left">I fixed this by downloading the latest [Intel Sata Rapid Storage Technology] drivers from the dell support site and extracting the [Intel Sata Rapid Storage Technology v10.1.2.1004_A01.exe] to a USB flash drive.</p>  <p align="left">When installing Microsoft Windows 7, choose Custom installation and load the AHCI driver from the USB flash drive. After that, Microsoft Windows 7 installed just fine.</p>  <p align="left">&#160;</p>  <p align="left">I am seeing pretty good results on the benchmarks: 556 MB/s Read and 500 MB write: </p>  <p align="left">&#160;</p>  <p align="left"><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/Capture.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="Capture" border="0" alt="Capture" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/Capture_thumb.png" width="533" height="626" /></a></p>
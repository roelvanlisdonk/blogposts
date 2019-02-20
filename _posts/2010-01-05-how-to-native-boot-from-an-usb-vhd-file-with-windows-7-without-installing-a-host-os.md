---
ID: 913
post_title: 'How to &#8220;native boot&#8221; from an USB VHD file with Windows 7, without installing a host OS'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/01/05/how-to-native-boot-from-an-usb-vhd-file-with-windows-7-without-installing-a-host-os/
published: true
post_date: 2010-01-05 20:15:13
---
<p>If you want to “native boot” from an USB VHD file with Windows 7, without installing a host OS, follow the tutorial on:   <br />    <br /><a title="http://www.windows7hacker.com/index.php/2009/08/windows-7-vhd-native-boot-without-any-hosting-operation-system/" href="http://www.windows7hacker.com/index.php/2009/08/windows-7-vhd-native-boot-without-any-hosting-operation-system/">http://www.windows7hacker.com/index.php/2009/08/windows-7-vhd-native-boot-without-any-hosting-operation-system/</a>    <br />    <br />Boot from the Windows 7 DVD, when it comes to the first screen, press SHIFT+F10 and you will get the comment window, the follow the steps:    <br /></p>  <ul>   <li>C:\&gt;DISKPART</li>    <li>DISKPART&gt;SEL VDISK File=C:\VHD\Win7.vhd </li>    <li>DISKPART&gt;ATTACH VDISK </li>    <li>DISKPART&gt;LIST VOL (This lists the drive letters and mappings, assuming F: maps to the VDISK) </li>    <li>DISKPART&gt;Exit </li>    <li>C:\&gt;Bcdboot F:\Windows </li> </ul>  <p>   <br />    <br />.    </p>
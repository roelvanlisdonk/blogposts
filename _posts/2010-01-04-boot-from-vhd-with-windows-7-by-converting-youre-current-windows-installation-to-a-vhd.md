---
ID: 904
post_title: 'Boot from USB VHD with Windows 7 by converting you&#8217;re current Windows installation to a VHD'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/01/04/boot-from-vhd-with-windows-7-by-converting-youre-current-windows-installation-to-a-vhd/
published: true
post_date: 2010-01-04 14:57:02
---
<p>   <br />Use the Microsoft Tool: Disk2vhd: <a title="http://technet.microsoft.com/en-us/sysinternals/ee656415.aspx" href="http://technet.microsoft.com/en-us/sysinternals/ee656415.aspx">http://technet.microsoft.com/en-us/sysinternals/ee656415.aspx</a> to convert you’re current Windows installation to a VHD.</p>  <p>Copy the created disk to you’re USB disk on E:\VHD</p>  <p>Open an <strong>elevated&#160; command prompt</strong> right click <strong>C:\Windows\System32\cmd.exe</strong> and click on “<strong>Run as administrator</strong>”</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image1.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb1.png" width="492" height="162" /></a> </p>  <p>Type: <strong>bcdedit /copy {current} /d “New VHD Description” </strong></p>  <p>This will return a GUID in my case <strong>{7dc00261-ee87-11de-8bd6-df41f0c5a8db}</strong> that must be used in the following statements:</p>  <p><strong>bcdedit /set {7dc00261-ee87-11de-8bd6-df41f0c5a8db} device vhd=[E:]\VHD\newvhd.vhd </strong></p>  <p><strong>bcdedit /set {7dc00261-ee87-11de-8bd6-df41f0c5a8db} osdevice vhd=[E:]\VHD\newvhd.vhd </strong></p>  <p><strong>bcdedit /set {7dc00261-ee87-11de-8bd6-df41f0c5a8db} detecthal on </strong></p>  <p>You can replace [E:]\VHD\newvhd.vhd with the path and name of your VHD. </p>  <p>After rebooting you should se the entry: “New VDH Description”</p>  <p>If you want to delete the entry enter: </p>  <p><strong>bcdedit /delete {GUID} /cleanup</strong></p>
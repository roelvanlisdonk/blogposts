---
ID: 865
post_title: >
  How to share a printer on Windows 7 with
  a VMware Workstation 7 image on a NAT
  Network Connection
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/12/18/how-to-share-a-printer-on-windows-7-with-a-vmware-workstation-7-image-on-a-nat-network-connection/
published: true
post_date: 2009-12-18 16:52:59
---
<p>If you want to print from a VMware Workstation 7 image, which uses a NAT network connection. You can use the default Windows&#160; printer sharing.   <br />On the host machine: start &gt; devices and printers &gt; add a printer &gt; add a local printer &gt; create a new port &gt; Standard TCP/IP Port &gt;     <br />    <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image15.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image_thumb15.png" width="406" height="299" /></a>     <br />    <br />Enter the ip adres of the network printer. Click on OK    <br />Right click the created printer &gt; Printer Properties &gt; Sharing &gt; Check “Share this printer”    <br />    <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image16.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/12/image_thumb16.png" width="395" height="438" /></a>     <br />    <br />On the VMware image:    <br />    <br />start &gt; devices and printers &gt; add a printer &gt; add a network printer     <br />    <br />It will automatically show the printer, because the host computer and the VMware image share a private network with a NAT network connection    </p>
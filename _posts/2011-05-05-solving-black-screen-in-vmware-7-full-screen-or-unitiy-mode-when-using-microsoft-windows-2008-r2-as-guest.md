---
ID: 2004
post_title: >
  Solving black screen in VMWare 7 full
  screen or unitiy mode, when using
  Microsoft Windows 2008 R2 as guest
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/05/05/solving-black-screen-in-vmware-7-full-screen-or-unitiy-mode-when-using-microsoft-windows-2008-r2-as-guest/
published: true
post_date: 2011-05-05 13:42:21
---
<p>Only normal en quick switch modus worked for me in VMWare 7, when using Microsoft Windows 2008 R2 as a guest OS.</p>  <p>Enabling 3D acceleration on de virtual machine monitor solved this problem.</p>  <p>Open you’re virtual machine and in the top menu go to: </p>  <p>- VM &gt; Settings &gt; Display &gt; Check [Accelerate 3D graphics]</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image_thumb.png" width="580" height="510" /></a></p>
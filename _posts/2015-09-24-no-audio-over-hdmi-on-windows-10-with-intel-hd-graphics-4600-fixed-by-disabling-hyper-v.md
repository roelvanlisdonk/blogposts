---
ID: 4601
post_title: 'No audio over HDMI on Windows 10 with Intel&reg; HD Graphics 4600 fixed by disabling Hyper-V'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/09/24/no-audio-over-hdmi-on-windows-10-with-intel-hd-graphics-4600-fixed-by-disabling-hyper-v/
published: true
post_date: 2015-09-24 19:35:03
---
<p>I have spend literarily days figuring out this problem. When I fresh install Windows 10 on my Shuttle DS81 I get audio over HDMI when connecting my LG TV to it, then something changes on my system and I got no audio over HDMI.</p>  <p>&#160;</p>  <p><strong><font size="4">The fix</font></strong></p>  <p>Turns out that disabling Hyper-V fixes the problem.</p>  <p>&#160;</p>  <p>I think installing Microsoft Visual Studio 2015 enabled Hyper-V but I’m not sure.</p>  <p>On this device audio over HDMI is more important then Hyper-V, but I still like Microsoft to fix this problem. This problem exists since a technical preview somewhere begin 2015 and even exist in the current release build of Windows 10.</p>  <p>&#160;</p>  <p>The weird thing is, that every things seems to work fine, the green bars are showing, just no sound over HDMI:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/09/image7.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/09/image_thumb7.png" width="560" height="367" /></a></p>
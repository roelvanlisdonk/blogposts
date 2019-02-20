---
ID: 2171
post_title: 'Solving: No microphone sound in Skype, when using remote desktop in Windows 7: No audio devices are installed.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/10/13/solving-no-microphone-sound-in-skype-when-using-remote-desktop-in-windows-7-no-audio-devices-are-installed-windows-7/
published: true
post_date: 2011-10-13 17:12:48
---
<p>I was using Microsoft Remote Desktop on a Microsoft Windows 7 machine to remotely control an other Windows 7 machine an I was running Skype on the remote machine. There was coming sound through the boxes of the local machine, but the microphone was not recorded even when the settings of the Local Resources where: Remote audio playback [Play on this computer] and Remote audio recording [Record from this computer].</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/10/image3.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/10/image_thumb3.png" width="377" height="682" /></a></p>  <p>&#160;</p>  <p align="left">The problem was found in the control panel &gt; sound &gt; recording &gt; Select a recording device below to modify its settings:</p>  <p align="left">this list was empty.</p>  <p align="left">&#160;</p>  <p align="left"><strong>Solution</strong></p>  <p align="left">After setting the registry key [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp\fDisableAudioCapture] to [0] on the remote machine and reconnecting the problem was solved.</p>
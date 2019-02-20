---
ID: 2259
post_title: >
  How to change Caps Lock key to Shift key
  in Microsoft Windows 7 or disable it
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/11/29/how-to-change-caps-lock-key-to-shift-key-in-microsoft-windows-7-or-disable-it/
published: true
post_date: 2011-11-29 11:48:02
---
<p>If you want to change the Caps Lock key to a Shift key, use the following registry changes:</p>  <p>&#160;</p>  <p>Windows Registry Editor Version 5.00</p>  <p>[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout]   <br />&quot;Scancode Map&quot;=hex:00,00,00,00,00,00,00,00,02,00,00,00,2a,00,3a,00,00,00,00,00</p>  <p>&#160;</p>  <p>If you want to completely disable the Caps Lock key, use the following registry changes:</p>  <p>Windows Registry Editor Version 5.00</p>  <p>[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout]   <br />&quot;Scancode Map&quot;=-    <br /></p>  <p>&#160;</p>  <p>After applying the registry change, reboot you’re system for the changes to take effect.</p>  <p>&#160;</p>  <p>Found at : <a title="http://www.howtogeek.com/howto/windows-vista/disable-caps-lock-key-in-windows-vista/" href="http://www.howtogeek.com/howto/windows-vista/disable-caps-lock-key-in-windows-vista/">http://www.howtogeek.com/howto/windows-vista/disable-caps-lock-key-in-windows-vista/</a></p>
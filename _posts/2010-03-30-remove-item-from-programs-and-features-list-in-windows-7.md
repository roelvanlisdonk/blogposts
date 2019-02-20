---
ID: 1179
post_title: >
  Remove item from Programs and Features
  list in Windows 7
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/30/remove-item-from-programs-and-features-list-in-windows-7/
published: true
post_date: 2010-03-30 15:08:00
---
<p>If the uninstallation of an program fails, the item will not be removed from the “Programs and Features” list on the Control Panel in Windows 7.</p>  <p>To remove the item, remove the item from the registry key:</p>  <p>Windows 7 x64</p>  <p><strong>HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall</strong></p>  <p>&#160;</p>  <p>Windows 7 x86</p>  <p><strong>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall</strong></p>  <p>&#160;</p>  <p>Note</p>  <p>Removing the key will only remove the item form the “Programs and Features” list, if you want to re-install the program you should also find the productcode and the corresponding upgrade code, then remove the entry from: </p>  <p><strong>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Installer\UpgradeCodes</strong></p>
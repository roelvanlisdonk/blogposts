---
ID: 4308
post_title: >
  LAN on Hyper-V virtual machine not
  working on Windows 10
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/03/25/lan-on-hyper-v-virtual-machine-not-working-on-windows-10/
published: true
post_date: 2015-03-25 10:06:10
---
<p>After an Windows 10 update, my Hyper-V virtual machines, did not have a working internet connection.</p>  <p>To fix this problem I had to:</p>  <p>- Shutdown all virtual machines</p>  <p>- Remove all network adapters of all virtual machines</p>  <p>- Remove all virtual switches in Hyper-V</p>  <p>- Reboot host</p>  <p>- Create new virtual switch</p>  <p>- Add network adapters that use the new virtual switch to all virtual machines</p>  <p>- Reboot the host</p>  <p>- Start virtual machines</p>  <p>&#160;</p>  <p>After these steps my virtual machines were running with working internet connections.</p>
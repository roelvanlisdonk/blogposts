---
ID: 4700
post_title: 'Fixed: Hyper-V virtual machine reports network cable unplugged on Windows 10'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/12/16/fixed-hyper-v-virtual-machine-reports-network-cable-unplugged-on-windows-10/
published: true
post_date: 2015-12-16 10:33:14
---
<p>After importing a Hyper-V virtual machine from a Windows 10 machine to an other Windows 10 machine, the Hyper-V virtual machine reported a network cable unplugged. This was fixed by running the <strong>netcfg –d</strong> command in a cmd on the destination Windows 10 machine and re-creating the virtual switch afterwards. </p>
---
ID: 1765
post_title: >
  Disable or Enable network adapter from
  the command line in Windows 7
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/10/22/disable-or-enable-network-adapter-from-the-command-line-in-windows-7/
published: true
post_date: 2010-10-22 08:18:58
---
<p>If you want to disable or enable a specific network adapter from the command line, you can use:</p>  <p>netsh interface set interface &quot;Local Area Connection&quot; DISABLED</p>  <p>netsh interface set interface &quot;Local Area Connection&quot; ENABLED</p>
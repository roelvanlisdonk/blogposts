---
ID: 5154
post_title: 'Map network drive in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2018/01/04/map-network-drive-in-c/
published: true
post_date: 2018-01-04 09:33:46
---
<span style="color: green; font-family: Consolas; font-size: 9pt;">// Create network drive mapping<span style="color: black;">
</span></span>

<span style="color: black; font-family: Consolas; font-size: 9pt;">System.Diagnostics.Process.Start(<span style="color: #a31515;">"net.exe"<span style="color: black;">, <span style="color: maroon;">@"use K: ""<a href="file:///\\acc-arbovitale.zorgvandezaak.nl\Websites_email\zvdzo">\\my.server.com\Websites\Mail</a>"" /user:MyDomain\admin MySuperSecretPassword"<span style="color: black;">).WaitForExit();
</span></span></span></span></span>

<span style="color: green; font-family: Consolas; font-size: 9pt;">// Remove network drive mapping<span style="color: black;">
</span></span>

<span style="font-family: Consolas; font-size: 9pt;">System.Diagnostics.Process.Start("net.exe", @"use K: /delete").WaitForExit();</span>
---
ID: 1152
post_title: >
  To combine (join) physical and relative
  filesystem paths in PowerShell, use
  Join-Path
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/25/to-combine-join-physical-and-relative-filesystem-paths-in-powershell-use-join-path/
published: true
post_date: 2010-03-25 11:58:23
---
<p>If you want to combine the physical path C:\ with a relative path “Temp” in PowerShell, Use Join-Path</p>  <p>&#160;</p>  <p>PS C:\Users\rLisdonk&gt; Join-Path &quot;C:\&quot; &quot;\Temp&quot;   <br />C:\Temp    <br />PS C:\Users\rLisdonk&gt; Join-Path &quot;C:\&quot; &quot;Temp&quot;    <br />C:\Temp    <br />PS C:\Users\rLisdonk&gt; Join-Path &quot;C:&quot; &quot;Temp&quot;    <br />C:\Temp</p>
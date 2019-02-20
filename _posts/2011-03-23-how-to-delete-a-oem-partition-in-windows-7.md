---
ID: 1908
post_title: >
  How to delete a OEM partition in Windows
  7
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/03/23/how-to-delete-a-oem-partition-in-windows-7/
published: true
post_date: 2011-03-23 08:51:40
---
<p>See: <a title="http://jaredheinrichs.com/how-to-delete-oem-partition.html" href="http://jaredheinrichs.com/how-to-delete-oem-partition.html">http://jaredheinrichs.com/how-to-delete-oem-partition.html</a></p>  <p>If you get the error: </p>  <p>Virtual Disk Service Error:   <br />The operation is not supported by the object.</p>  <p>&#160;</p>  <p>Make sure you’re disk is not a dynamic disk.   <br />In mine case the disk was a dynamic disk en I converted it back to a basic disk, by using diskpart:    <br />select disk 0    <br />convert basic</p>  <p>&#160;</p>  <p>After converting the disk back to a basic disk I followed the steps on <a title="http://jaredheinrichs.com/how-to-delete-oem-partition.html" href="http://jaredheinrichs.com/how-to-delete-oem-partition.html">http://jaredheinrichs.com/how-to-delete-oem-partition.html</a></p>
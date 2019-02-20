---
ID: 3227
post_title: 'Going from 15.000 requests p/s to 250.000 requests p/s with Microsoft SQL Server&ndash;Hekaton'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/06/04/going-from-15-000-requests-ps-to-250-000-requests-ps-with-microsoft-sql-serverhekaton/
published: true
post_date: 2013-06-04 09:21:41
---
<p>Microsoft SQL Server up until version 2012, is build on the presumption that the data will be stored on hard disks and the price of this storage is high not even considering the price of memory, so trade offs are made to make SQL Server 2012 run on this kind of hardware, but what if we forget this and look at modern hardware, with SSD’s, &quot;cheap&quot; storage and memory, how would SQL Server then be build….? Meet Microsoft SQL Server Hekaton:</p>  <p>&#160;</p>  <p>Some of the key features that I found interesting:</p>  <p><strong></strong></p>  <p><strong>MVCC = multiversion concurrency control</strong> </p>  <p>Readers don’t block writers, because of multiple version of data will be stored, but only one will be the last.</p>  <p>&#160;</p>  <p><strong>In-memory</strong></p>  <p>Just by changing a property on a table, you can transform this data structure to an in-memory data structure, without the need of changing any of your existing code. </p>  <p>&#160;</p>  <p><strong>Optimized for SSD (Bw-tree)</strong></p>  <p>&quot;We had an 'aha' moment,&quot; Lomet recalls, &quot;when we realized that a single table that maps page identifiers to page locations would enable both latch-free page updating and log-structured page storage on flash memory. The other highlight, of course, was when we got back performance results that were stunningly good.&quot;</p>  <p>&#160;</p>  <p><strong>More info at</strong></p>  <p><a href="http://research.microsoft.com/en-us/news/features/hekaton-122012.aspx">http://research.microsoft.com/en-us/news/features/hekaton-122012.aspx</a></p>
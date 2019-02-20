---
ID: 5314
post_title: 'Split string and get row number / index by using string_split in >= SQL Server 2016'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2019/01/07/split-string-and-get-row-number-index-by-using-string_split-in-sql-server-2016/
published: true
post_date: 2019-01-07 21:47:44
---
<span style="color:blue; font-family:Consolas; font-size:9pt; background-color:white">declare<span style="color:black"> @name <span style="color:blue">nvarchar<span style="color:gray">(<span style="color:fuchsia">max<span style="color:gray">)<span style="color:black">
<span style="color:gray">=<span style="color:black">
<span style="color:red">'test.d.f.g.hf.ddddd'<span style="color:black">
</span></span></span></span></span></span></span></span></span></span></span>

<span style="color:blue; font-family:Consolas; font-size:9pt; background-color:white">declare<span style="color:black"> @items <span style="color:blue">table<span style="color:gray">(<span style="color:black">
</span></span></span></span></span>

<span style="color:black; font-family:Consolas; font-size:9pt; background-color:white">    id <span style="color:blue">int<span style="color:black">
<span style="color:blue">identity<span style="color:gray">(<span style="color:black">1<span style="color:gray">,<span style="color:black">1<span style="color:gray">)<span style="color:black">
<span style="color:gray">not<span style="color:black">
<span style="color:gray">null<span style="color:black">
</span></span></span></span></span></span></span></span></span></span></span></span></span></span>

<span style="color:gray; font-family:Consolas; font-size:9pt; background-color:white">,<span style="color:black">   part <span style="color:blue">nvarchar<span style="color:gray">(<span style="color:fuchsia">max<span style="color:gray">)<span style="color:black">
</span></span></span></span></span></span></span>

<span style="color:gray; font-family:Consolas; font-size:9pt; background-color:white">);<span style="color:black">
</span></span>

<span style="color:blue; font-family:Consolas; font-size:9pt; background-color:white">insert<span style="color:black">
<span style="color:blue">into<span style="color:black"> @items<span style="color:blue">
<span style="color:gray">(<span style="color:black">part<span style="color:gray">)<span style="color:black">
</span></span></span></span></span></span></span></span></span>

<span style="color:blue; font-family:Consolas; font-size:9pt; background-color:white">select<span style="color:black"> [value]
</span></span>

<span style="color:blue; font-family:Consolas; font-size:9pt; background-color:white">from<span style="color:black">
<span style="color:fuchsia">string_split<span style="color:gray">(<span style="color:black">@name<span style="color:gray">,<span style="color:black">
<span style="color:red">'.'<span style="color:gray">)<span style="color:black">
</span></span></span></span></span></span></span></span></span></span>

<span style="color:blue; font-family:Consolas; font-size:9pt; background-color:white">where<span style="color:black">
<span style="color:fuchsia">rtrim<span style="color:gray">(<span style="color:black">[value]<span style="color:gray">)<span style="color:black">
<span style="color:gray">&lt;&gt;<span style="color:black">
<span style="color:red">''<span style="color:gray">;<span style="color:black">
</span></span></span></span></span></span></span></span></span></span></span></span>

<span style="color:blue"><span style="font-family:Consolas; font-size:9pt; background-color:white">select<span style="color:black">
<span style="color:gray">*<span style="color:black">
<span style="color:blue">from<span style="color:black"> @items</span></span></span></span></span></span>
</span>

This will result in:

<img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2019/01/010719_2047_Splitstring1.png" alt="">
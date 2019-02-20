---
ID: 4632
post_title: >
  How to prevent data to be changed, when
  copying over linked server connection in
  SQL Server
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/10/08/how-to-prevent-data-to-be-changed-when-copying-over-linked-server-connection-in-sql-server/
published: true
post_date: 2015-10-08 09:29:22
---
<p>&#160;</p>  <p>When I was inserting and updating data over a SQL Server linked server connection, special characters in “strings” were altered. </p>  <p>&#160;</p>  <p>A character “ë” was changed to the character “Ù”.</p>  <p>&#160;</p>  <p>Now the first thing I checked was the collation on both databases and columns.</p>  <p>They were exactly the same, so I expected the data NOT to be altered.</p>  <p>I think this is a bug in SQL Server, but I have a workaround: set the collation of the linked server connection:</p>  <p>&#160;</p>  <p>use master</p>  <p>go</p>  <p>exec sp_serveroption '93_WGD', 'collation compatible', 'false'</p>  <p>go</p>  <p>exec sp_serveroption '93_WGD', 'use remote collation', 'false'</p>  <p>go</p>  <p>exec sp_serveroption '93_WGD', 'collation name', 'Latin1_General_BIN2'</p>  <p>go</p>
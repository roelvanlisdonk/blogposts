---
ID: 665
post_title: >
  After updating WordPress to 2.8.4 I get
  the XMLRPC 500 Internal Server Error,
  when posting with Microsoft Windows
  LiveWriter
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/08/31/after-updating-wordpress-to-2-8-4-i-get-the-xmlrpc-500-internal-server-error-when-posting-with-microsoft-windows-livewriter/
published: true
post_date: 2009-08-31 12:02:05
---
<p>The solution is to change the type of the column post_parent:   <br /></p>  <p>cd &quot;C:\Program Files (x86)\MySQL\MySQL Server 5.1\bin\&quot;</p>  <p>mysql.exe –u root -p    <br />Enter password: *********************** </p>  <p>mysql&gt; use MyWordpressDatabase    <br />Database changed     <br />mysql&gt; ALTER TABLE wp_posts CHANGE post_parent post_parent BIGINT;</p>  <p>   <br />See: <a title="http://ardentdev.com/fix-for-wordpress-xmlrpc-500-internal-server-error/" href="http://ardentdev.com/fix-for-wordpress-xmlrpc-500-internal-server-error/">http://ardentdev.com/fix-for-wordpress-xmlrpc-500-internal-server-error/</a></p>
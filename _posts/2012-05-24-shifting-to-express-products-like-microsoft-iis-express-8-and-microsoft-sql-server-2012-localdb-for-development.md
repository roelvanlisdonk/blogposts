---
ID: 2715
post_title: >
  Shifting to express products like
  Microsoft IIS Express 8 and Microsoft
  SQL Server 2012 LocalDb for development.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/05/24/shifting-to-express-products-like-microsoft-iis-express-8-and-microsoft-sql-server-2012-localdb-for-development/
published: true
post_date: 2012-05-24 22:02:24
---
<p>Most express products have some things in common:</p>  <p>- Contain the same features as the full product (except for some limitations like, no more then 4GB memory or no more then 10 users etc.)</p>  <p>- Free of charge</p>  <p>- Lightweight</p>  <p>- User profile specific (multiple users on one machine have independent product configuration and processes)</p>  <p>These products are created mainly for development purposes.</p>  <p>&#160;</p>  <p><strong>Advantages</strong></p>  <p>More and more I am shifting to these express products for the O in OTAP and for the build servers, because these products have the following advantages:</p>  <p>- Free of charge.</p>  <p>- No configuration.</p>  <p>- Fast and lightweight installation.</p>  <p>- Performance improvements for DEV en build server machines.</p>  <p>- Build servers can use clean instances to run integration tests.</p>  <p>- Easily to restore to new instance.   <br />When a per user instance is corrupted it’s very easy to restore it.</p>  <p>- <strong>Multiple users can work on one virtual machine, without interfering with each other.     <br /></strong>So each developer can change all the things he or she wants to research some new code, without breaking a shared instance of IIS or SQL Server.</p>  <p>&#160;</p>  <p>Of course for the T, the A and P in OTAP, I use the full products. </p>
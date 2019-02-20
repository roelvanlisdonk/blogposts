---
ID: 1681
post_title: New features in ASP .NET 4.0 that I use
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/08/25/new-features-in-asp-net-4-0-that-i-use/
published: true
post_date: 2010-08-25 10:09:29
---
<p>After doing some projects for customers with ASP .NET 4.0, what are the new features that I used in the real world?</p>  <ul>   <li><strong>SQL cache invalidation</strong>: this means that when the result set from SQL Server changes, the output cache is triggered to change, and the end user always sees the latest result set. The data presented is never stale</li>    <li>ASP.NET 4 provides <strong>64-bit support</strong>. This means that you can run your ASP.NET applications on 64-bit      <br />Intel or AMD processors.</li>    <li><strong>ADO .NET Entity Framework</strong>, used for business entity- and data layer.</li>    <li><strong>ASP.NET Dynamic Data</strong>, used for generating the administration pages of an web application.</li>    <li><strong>WCF Data Services</strong>, to create, update and delete data in the database, via a RESTful service</li>    <li><strong>Health monitoring system</strong>, used in addition to SCOM to monitor the health of the system. (log: application starts and stops, failed logins, unhandled exceptions etc.)</li>    <li><strong>WebConfigurationManager</strong>, to read and write to the web.config, changing settings.</li> </ul>
---
ID: 3144
post_title: 'Fixing SqlDependency Query Notification subscription failure: info=&quot;set options&quot; database_id=&quot;0&quot; in SQL Server 2012'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/01/31/fixing-sqldependency-query-notification-subscription-failure-infoset-options-database_id0-in-sql-server-2012/
published: true
post_date: 2013-01-31 21:46:40
---
<p>Registering a query for Query Notification requires the database connection on which the subscription is made to have the correct SET OPTIONS enabled:</p>  <p>ANSI_NULLS ON   <br />ANSI_PADDING ON    <br />ANSI_WARNINGS ON    <br />CONCAT_NULL_YIELDS_NULL ON    <br />QUOTED_IDENTIFIER ON    <br />NUMERIC_ROUNDABORT OFF    <br />ARITHABORT ON</p>  <p>&#160;</p>  <p>In my case the SET OPTION ARITHABORT was set to OFF.</p>  <p>When tracing the Microsoft SQL Server 2012 database with the SQL Server Profile I noticed the following record:</p>  <p>&lt;qnev:QNEvent xmlns:qnev=&quot;<a href="http://schemas.microsoft.com/SQL/Notifications/QueryNotificationProfiler&quot;">http://schemas.microsoft.com/SQL/Notifications/QueryNotificationProfiler&quot;</a>&gt;    <br />&#160;&#160;&#160; &lt;qnev:EventText&gt;subscription fired&lt;/qnev:EventText&gt;    <br />&#160;&#160;&#160; &lt;qnev:SubscriptionID&gt;0&lt;/qnev:SubscriptionID&gt;    <br />&#160;&#160;&#160; &lt;qnev:NotificationMsg&gt;    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; ﻿&amp;lt;qn:QueryNotification     <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; xmlns:qn=&quot;<a href="http://schemas.microsoft.com/SQL/Notifications/QueryNotification&quot;">http://schemas.microsoft.com/SQL/Notifications/QueryNotification&quot;</a>    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; id=&quot;0&quot;    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; type=&quot;subscribe&quot;    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; source=&quot;statement&quot;    <br /><strong>&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; info=&quot;set options&quot;     <br /></strong>&#160;&#160;&#160;&#160;&#160;&#160;&#160; database_id=&quot;0&quot;    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; sid=&quot;0x01&quot;&amp;gt;    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; &amp;lt;qn:Message&amp;gt;    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; 62ed343a-0149-4774-8dd1-b3da8f5a4840;    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; fc208372-6da2-4083-9866-7ac9fb9e5d38&amp;lt;    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; /qn:Message&amp;gt;&amp;lt;    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; /qn:QueryNotification&amp;gt;    <br />&#160;&#160;&#160; &lt;/qnev:NotificationMsg&gt;    <br />&#160;&#160;&#160; &lt;qnev:BrokerDlg&gt;BFCF056A-C16B-E211-B799-005056A36108&lt;/qnev:BrokerDlg&gt;    <br />&lt;/qnev:QNEvent&gt;</p>  <p>&#160;</p>  <p>And when I enabled more events in the trace, I found a record just before this subscription failure message:</p>  <p>-- network protocol: TCP/IP   <br />set quoted_identifier on    <br /><strong>set arithabort off</strong>    <br />set numeric_roundabort off    <br />set ansi_warnings on    <br />set ansi_padding on    <br />set ansi_nulls on    <br />set concat_null_yields_null on    <br />set cursor_close_on_commit off    <br />set implicit_transactions off    <br />set language us_english    <br />set dateformat mdy    <br />set datefirst 7    <br />set transaction isolation level read committed</p>  <p>&#160;</p>  <p>So now I knew the SET OPTION arithabort was wrong.</p>  <p>&#160;</p>  <p><strong>Solution</strong></p>  <p>Setting the Database option Arithmetic Abort Enabled to True fixed the problem.</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/01/image4.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/01/image_thumb4.png" width="523" height="240" /></a></p>
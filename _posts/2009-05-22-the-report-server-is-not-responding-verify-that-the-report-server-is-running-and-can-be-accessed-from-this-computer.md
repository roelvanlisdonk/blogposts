---
ID: 440
post_title: >
  The report server is not responding.
  Verify that the report server is running
  and can be accessed from this computer
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/22/the-report-server-is-not-responding-verify-that-the-report-server-is-running-and-can-be-accessed-from-this-computer/
published: true
post_date: 2009-05-22 13:25:47
---
<p>After changing the websitename, hostheader or computername of a Microsoft Reporting Services Server, you get the error: <strong>The report server is not responding. Verify that the report server is running and can be accessed from this computer.      <br /></strong>    <br />This error occurs, because the UrlRoot element in the RSReportServer.config is not changed automaticly, when you change your computername or website hostheader.     <br />Open the <strong>RSReportServer.config</strong> in the folder: <strong>C:\Program Files\Microsoft SQL Server\MSSQL.2\Reporting Services\ReportServer</strong>    <br />Change the <strong>UrlRoot</strong> element to the correct name</p>  <p>Open <strong>RSWebApplication.config</strong> file and, if necessary, modify the <b>ReportServerUrl</b> setting to reflect the new server name. Note that this setting is not used in every installation. If it is empty, do nothing. </p>  <p>For example in: C:\Program Files\Microsoft SQL Server\<strong>MSSQL.#</strong>\Reporting Services\ReportServer open </p>  <p><strong>RSReportServer.config</strong></p>  <p>old value:    <br />&lt;UrlRoot&gt;http://&lt;servername&gt;/reportserver&lt;/UrlRoot&gt; </p>  <p>new value:    <br />&lt;UrlRoot&gt;<a href="http://10.10.10.11/reportserver">http://&lt;hostneader&gt;/reportserver</a>&lt;/UrlRoot&gt; </p>  <p>For example in: C:\Program Files\Microsoft SQL Server\<strong>MSSQL.#</strong>\Reporting Services\ReportManager open </p>  <p><strong>RSWebApplication.config</strong></p>  <p>old value:    <br />&lt;ReportServerUrl&gt;&lt;/ReportServerUrl&gt;     <br />&lt;ReportServerVirtualDirectory&gt;ReportServer&lt;/ReportServerVirtualDirectory&gt; </p>  <p>new value:    <br />&lt;ReportServerUrl&gt;<a href="http://10.10.10.11/reportserver">http://&lt;hostneader&gt;/reportserver</a>&lt;/ReportServerUrl&gt;     <br />&lt;ReportServerVirtualDirectory&gt;&lt;/ReportServerVirtualDirectory&gt; </p>  <p>Note: It's very important that only one of the two values is filled, else an error will occur. </p>  <p>Run iisreset /noforce and you're now using multiple instance of Reporting Services on the same machine. </p>
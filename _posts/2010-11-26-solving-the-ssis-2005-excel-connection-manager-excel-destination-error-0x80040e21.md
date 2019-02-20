---
ID: 1842
post_title: >
  Solving the SSIS 2005 Excel Connection
  Manager (Excel Destination) Error
  0x80040E21
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/11/26/solving-the-ssis-2005-excel-connection-manager-excel-destination-error-0x80040e21/
published: true
post_date: 2010-11-26 16:23:04
---
<p>I was getting as 0x80040E21 error on a SSIS 2005 package when exporting some rows to an Excel file.</p>  <p>&#160;</p>  <p>In my case this was caused by an input column of the type varchar(max) after converting this column in my t-sql query to a varchar(1024) column the error was resolved.</p>  <p>&#160;</p>  <p><strong>Error</strong></p>  <p>Error: 0xC0202009 at Data Flow Task, Excel Destination [16]: SSIS Error Code DTS_E_OLEDBERROR.&#160; An OLE DB error has occurred. Error code: 0x80040E21.   <br />Error: 0xC0202025 at Data Flow Task, Excel Destination [16]: Cannot create an OLE DB accessor. Verify that the column metadata is valid.    <br />Error: 0xC004701A at Data Flow Task, DTS.Pipeline: component &quot;Excel Destination&quot; (16) failed the pre-execute phase and returned error code 0xC0202025.</p>
---
ID: 1843
post_title: >
  Solving the SSIS 2005 Excel Connection
  Manager error 0x80040E09
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/11/26/solving-the-ssis-2005-excel-connection-manager-error-0x80040e09/
published: true
post_date: 2010-11-26 16:26:49
---
<p>I was getting a 0x80040E09 error, when exporting some rows to an Excel file in SSIS 2005. This was caused by the destination Excel file being read-only. After I cleared the read-only checkbox on the file, the error was resolved.</p>  <p>&#160;</p>  <p><strong>Error</strong></p>  <p>Error: 0xC0202009 at Data Flow Task, Excel Destination [16]: SSIS Error Code DTS_E_OLEDBERROR.&#160; An OLE DB error has occurred. Error code: 0x80040E09.   <br />Error: 0xC0047022 at Data Flow Task: SSIS Error Code DTS_E_PROCESSINPUTFAILED.&#160; The ProcessInput method on component &quot;Excel Destination&quot; (16) failed with error code 0xC0202009. The identified component returned an error from the ProcessInput method. The error is specific to the component, but the error is fatal and will cause the Data Flow task to stop running.&#160; There may be error messages posted before this with more information about the failure.    <br />Error: 0xC0047021 at Data Flow Task: SSIS Error Code DTS_E_THREADFAILED.&#160; Thread &quot;WorkThread0&quot; has exited with error code 0xC0202009.&#160; There may be error messages posted before this with more information on why the thread has exited.</p>
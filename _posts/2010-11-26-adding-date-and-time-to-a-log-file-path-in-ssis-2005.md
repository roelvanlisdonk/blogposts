---
ID: 1839
post_title: >
  Adding date and time to a log file path
  in SSIS 2005
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/11/26/adding-date-and-time-to-a-log-file-path-in-ssis-2005/
published: true
post_date: 2010-11-26 10:31:09
---
<p>Right click your log file connection, click on properties</p>  <p>In the property windows click on Expressions &gt; ConnectionString</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/11/image16.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/11/image_thumb16.png" width="704" height="529" /></a> </p>  <p>&#160;</p>  <p><strong> Expression</strong></p>  <p>Add the expression:</p>  <p>(DT_WSTR,1000)   <br />(    <br />&#160; &quot;C:\Temp\&quot; +    <br />&#160; RIGHT(&quot;0&quot; + (DT_STR,4,1252) DATEPART(&quot;year&quot;,GETDATE()),4) +     <br />&#160; RIGHT(&quot;0&quot; + (DT_STR,2,1252) DATEPART(&quot;month&quot;,GETDATE()),2) +     <br />&#160; RIGHT(&quot;0&quot; + (DT_STR,2,1252) DATEPART(&quot;day&quot;,GETDATE()),2) +     <br />&#160; RIGHT(&quot;0&quot; + (DT_STR,2,1252) DATEPART(&quot;hour&quot;,GETDATE()),2) +     <br />&#160; RIGHT(&quot;0&quot; + (DT_STR,2,1252) DATEPART(&quot;minute&quot;,GETDATE()),2) +     <br />&#160; RIGHT(&quot;0&quot; + (DT_STR,2,1252) DATEPART(&quot;second&quot;,GETDATE()),2) +     <br />&#160; &quot;.log&quot;    <br />)</p>  <p>&#160;</p>  <p><strong>Result</strong></p>  <p>Result will be: C:\Temp\20101126121212.log</p>
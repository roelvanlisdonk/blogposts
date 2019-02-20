---
ID: 1271
post_title: 'How to filter &ndash; reject records during Microsoft SQL Server Integration Services (SSIS) import of a flat file'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/04/22/how-to-filter-reject-records-during-microsoft-sql-server-integration-services-ssis-import-of-a-flat-file/
published: true
post_date: 2010-04-22 11:34:21
---
<p>If you want to filter – reject records during a Microsoft SQL Server Integration Services (SSIS) import of a flat file, you can use the <strong>Conditional Split Data Flow Transformation</strong>. If the flat file is a CSV file with the following contents:</p>  <p>&#160;</p>  <p><strong>Flat file contents</strong></p>  <p>EEEtest,0,1,2</p>  <p>000000,0,1,2</p>  <p>blabla test,0,1,2</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/04/image26.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/04/image_thumb26.png" width="604" height="584" /></a> </p>  <p>&#160;</p>  <p><strong>Result</strong></p>  <p>EEEtest,0,1,2</p>  <p>blabla test,0,1,2</p>  <p>&#160;</p>  <p>One row is filtered, because the first column has a value of “000000” and thus starts with “0000”, see the Condition expression</p>  <p>&#160;</p>  <p><strong>Complete dataflow screendump</strong></p>  <p><strong></strong></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/04/image27.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/04/image_thumb27.png" width="704" height="637" /></a></p>
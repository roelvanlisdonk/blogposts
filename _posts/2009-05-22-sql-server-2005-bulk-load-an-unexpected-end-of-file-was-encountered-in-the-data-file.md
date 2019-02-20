---
ID: 444
post_title: 'SQL Server 2005 Bulk load: An unexpected end of file was encountered in the data file.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/22/sql-server-2005-bulk-load-an-unexpected-end-of-file-was-encountered-in-the-data-file/
published: true
post_date: 2009-05-22 14:40:40
---
<p>If you import a file with bulk insert in a stored procedure on a Microsoft SQL Server 2005 database you can get the error:    <br />    <br /><strong>Error      <br /></strong>Msg 4832, Level 16, State 1, Line 1     <br />Bulk load: An unexpected end of file was encountered in the data file.     <br />Msg 7399, Level 16, State 1, Line 1     <br />The OLE DB provider &quot;BULK&quot; for linked server &quot;(null)&quot; reported an error. The provider did not give any information about the error.     <br />Msg 7330, Level 16, State 2, Line 1     <br />Cannot fetch a row from OLE DB provider &quot;BULK&quot; for linked server &quot;(null)&quot;.</p>  <p>In mine case, it was caused by the fact that I used to import the file with a rowterminator of &#8216;,&#8217; but the code expected a &#8216;\t&#8217; character as fieldterminator    <br /><strong>Code</strong>    <br />exec ('bulk insert dbo.ImportZ from ''' + @ZFile + ''' WITH (FIELDTERMINATOR = ''\t'', ROWTERMINATOR = ''\n'')')</p>  <p><strong>Incorrect fileformat</strong></p>  <p>4,ttt,5,4,1,,eeee    <br />4,ttt,5,4,1,,eeee     <br />4,ttt,5,4,1,,eeee     <br />etc</p>  <p>It can also be caused by a record that has less fields than expected</p>
---
ID: 2647
post_title: >
  How to insert the result of a stored
  procedure in a table variable
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/04/02/how-to-insert-the-result-of-a-stored-procedure-in-a-table-variable/
published: true
post_date: 2012-04-02 16:32:17
---
<p>Found the solution at:</p>  <p><a href="http://stackoverflow.com/questions/653714/how-to-select-into-temp-table-from-stored-procedure">http://stackoverflow.com/questions/653714/how-to-select-into-temp-table-from-stored-procedure</a></p>  <p>The following T-SQL code executes the system stored procedure sp_helpfile and stores the result in the table variable @temp.</p>  <p>&#160;</p>  <p>declare @temp table   <br />(    <br />&#160;&#160;&#160; name varchar(255),    <br />&#160;&#160;&#160; field varchar(255),    <br />&#160;&#160;&#160; filename varchar(255),    <br />&#160;&#160;&#160; filegroup varchar(255),    <br />&#160;&#160;&#160; size varchar(255),    <br />&#160;&#160;&#160; maxsize varchar(255),    <br />&#160;&#160;&#160; growth varchar(255),    <br />&#160;&#160;&#160; usage varchar(255)    <br />);    <br />INSERT @temp&#160; Exec sp_helpfile;    <br />select * from @temp;</p>
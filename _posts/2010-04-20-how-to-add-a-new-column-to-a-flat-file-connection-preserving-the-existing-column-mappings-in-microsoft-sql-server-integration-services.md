---
ID: 1260
post_title: >
  How to add a new column to a flat file
  connection preserving the existing
  column mappings in Microsoft SQL Server
  Integration Services
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/04/20/how-to-add-a-new-column-to-a-flat-file-connection-preserving-the-existing-column-mappings-in-microsoft-sql-server-integration-services/
published: true
post_date: 2010-04-20 13:54:59
---
<p>If you created a flat file connection in Microsoft SQL Server Integration Services and the structure of the input files changed (a column is added), you can add a column to you’re flat file connection, by following the steps below. This will preserve the existing column mappings and column renames, it will only add a column at the end.</p>  <ul>   <li>Double click on you’re flat file connection, this will open the “Flat File Connection Manager Editor”</li> </ul>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/04/image23.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/04/image_thumb23.png" width="504" height="454" /></a> </p>  <ul>   <li>Click on the New button</li>    <li>This will add a new column at the end, now you can change the Name, ColumnDelimiter, OutputColumnWidth etc.</li> </ul>  <p>&#160;</p>  <p>&#160;</p>  <p><strong>Note: The ColumnDelimiter value of the last column, should be the same as the RowDelimiter</strong></p>  <p>Because mine input file is a CSV file, with rows delimited by newlines and columns delimited by commas, I expected the ColumnDelimter of each column to be a comma, but when you try to change the ColumnDelimiter of the last field to a comma, you will get the exception: “The row delimiter cannot be the same as the column delimiter.” This is because the last ColumnDelimiter should be the same as the row delimiter. The last column of each record will be followed by the row delimiter and not a ColumnDelimiter.</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/04/image24.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/04/image_thumb24.png" width="504" height="456" /></a> </p> <a href="http://11011.net/software/vspaste"></a>
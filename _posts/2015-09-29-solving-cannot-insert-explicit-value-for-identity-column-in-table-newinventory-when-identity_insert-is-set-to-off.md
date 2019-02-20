---
ID: 4618
post_title: 'Solving: Cannot insert explicit value for identity column in table &#8216;NewInventory&#8217; when IDENTITY_INSERT is set to OFF.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/09/29/solving-cannot-insert-explicit-value-for-identity-column-in-table-newinventory-when-identity_insert-is-set-to-off/
published: true
post_date: 2015-09-29 10:34:59
---
<p>&#160;</p>  <p>&#160;</p>  <p><strong>SQL Server SET IDENTITY_INSERT</strong></p>  <p>At any time, <strong>only one table in a session can have the IDENTITY_INSERT property set to ON</strong>. If a table already has this property set to ON, and a SET IDENTITY_INSERT ON statement is issued for another table, Microsoft® SQL Server™ returns an error message that states SET IDENTITY_INSERT is already ON and reports the table it is set ON for.</p>  <p>&#160;</p>  <p>I was getting the message:</p>  <p>Msg 544, Level 16, State 1, Line 73   <br />Cannot insert explicit value for identity column in table 'NewInventory' when IDENTITY_INSERT is set to OFF.</p>  <p>This was caused by a script trying to set multiple tables to “IDENTITY_INSERT ON”.</p>
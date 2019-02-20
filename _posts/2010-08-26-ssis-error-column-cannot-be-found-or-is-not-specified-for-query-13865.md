---
ID: 1704
post_title: 'SSIS error: Column &quot;&hellip;&quot; cannot be found or is not specified for query (13865)'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/08/26/ssis-error-column-cannot-be-found-or-is-not-specified-for-query-13865/
published: true
post_date: 2010-08-26 15:46:46
---
<p>When I refreshed a SSIS package OLE DB Source, I got the error: column &quot;test&quot; cannot be found or is not specified for query (13865).</p>  <p>This was caused by the fact, that the query contained a column that did not exist anymore in de database.</p>  <p>Removing the column name in the SqlCommand resolved this error.</p>
---
ID: 1841
post_title: >
  Convert datetime to string in format
  HH:mm:ss in T-SQL
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/11/26/convert-datetime-to-string-in-format-hhmmss-in-t-sql/
published: true
post_date: 2010-11-26 14:12:43
---
<div>CONVERT(VARCHAR(8),GETDATE(),108)</div>
<div><strong>Result</strong></div>
<div>14:12:30</div>
<div><span style="color: gray;">
<strong>Other examples</strong></span></div>
<div>print convert(varchar(30),getdate(),121)
-- Result: 2011-05-09 12:04:31.883</div>
<div>print convert(varchar(30),getdate(),113)
-- Result: 29 Apr 2011 13:41:23:327</div>
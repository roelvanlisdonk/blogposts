---
ID: 578
post_title: >
  Formatting a date to a specific string
  (like dd-MM-YYYY) in Microsoft Excel VBA
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/06/24/formatting-a-date-to-a-specific-string-like-dd-mm-yyyy-in-microsoft-excel-vba/
published: true
post_date: 2009-06-24 17:07:09
---
<p>If you want to format a date to a specific date format, like dd-MM-YYYY in Microsoft Excel VBA, use:   <br /></p>  <p>Dim specificFormatedString as String   <br />specificFormatedString = Format(Date,&quot;DD-MM-YYYY&quot;)</p>
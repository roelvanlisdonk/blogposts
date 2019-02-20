---
ID: 417
post_title: 'Microsoft Excel &#8211; Calculate elapsed time from text &#8220;2008-02-11 09:45:12.023&#8221;'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/22/microsoft-excel-calculate-elapsed-time-from-text-2008-02-11-094512023/
published: true
post_date: 2009-05-22 08:01:25
---
<p>Select Kolom A en Format Cell as Text   <br />Enter the following values in colun A in Microsoft Excel    <br />A1 &quot;2008-02-11 09:45:12.023&quot;    <br />A2 &quot;2008-02-11 10:20:12.323&quot;    <br />Select Kolom B en Format Cell as TIME 37:30:55    <br />Enter the following formula in cell B2    <br />=(LEFT(RIGHT(A2;12);8))-(LEFT(RIGHT(A1;12);8))</p>
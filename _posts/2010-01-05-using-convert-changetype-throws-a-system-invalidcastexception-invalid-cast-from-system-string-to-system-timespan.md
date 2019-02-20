---
ID: 912
post_title: 'Using Convert.ChangeType throws a System.InvalidCastException: Invalid cast from &#039;System.String&#039; to &#039;System.TimeSpan&#039;'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/01/05/using-convert-changetype-throws-a-system-invalidcastexception-invalid-cast-from-system-string-to-system-timespan/
published: true
post_date: 2010-01-05 15:08:22
---
<p>When you use the function Convert.ChangeType on a TimeSpan, you will get a System.InvalidCastException: Invalid cast from 'System.String' to 'System.TimeSpan'. Use TimeSpan.FromDays   <br />TimeSpan.FromHours    <br />TimeSpan.FromMilliseconds    <br />TimeSpan.FromMinutes    <br />TimeSpan.FromSeconds    <br />TimeSpan.FromTicks</p>  <p>or the TimeSpan.TryParse method to convert a string to a TimeSpan.   </p>
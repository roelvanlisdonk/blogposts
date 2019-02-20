---
ID: 1231
post_title: >
  How to determine the datetime of the
  first day of the week
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/04/11/how-to-determine-the-datetime-of-the-first-day-of-the-week/
published: true
post_date: 2010-04-11 20:23:49
---
<p>If you want to determine the datetime of the first day of the week, you can use the following code:   <br /></p>  <pre class="code"><span style="color: green">// Get the first day of the week
</span><span style="color: #2b91af">DayOfWeek </span>firstDay = System.Threading.<span style="color: #2b91af">Thread</span>.CurrentThread.CurrentCulture.DateTimeFormat.FirstDayOfWeek; 
<span style="color: #2b91af">DateTime </span>firstDayOfWeekDateTime = <span style="color: #2b91af">DateTime</span>.Now;
<span style="color: blue">while </span>(firstDayOfWeekDateTime.DayOfWeek != firstDay)
{
    firstDayOfWeekDateTime = firstDayOfWeekDateTime.AddDays(-1);
}</pre>
<a href="http://11011.net/software/vspaste"></a>
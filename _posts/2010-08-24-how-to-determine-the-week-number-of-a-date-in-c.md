---
ID: 1680
post_title: 'How to determine the week number of a date in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/08/24/how-to-determine-the-week-number-of-a-date-in-c/
published: true
post_date: 2010-08-24 16:07:01
---
<p>If you want to get the week number of a date in C#, use the following function:</p>  <pre class="code"><p><font size="1"><span style="color: blue">private int </span>GetWeekNumber(<span style="color: #2b91af">DateTime </span>date)
{
<span style="color: blue"> return </span><span style="color: #2b91af">CultureInfo</span>.CurrentCulture.Calendar.GetWeekOfYear(date, <span style="color: #2b91af">CalendarWeekRule</span>.FirstFourDayWeek, <span style="color: #2b91af">DayOfWeek</span>.Monday);
}</font></p><p>&#160;</p></pre>
<a href="http://11011.net/software/vspaste"></a>
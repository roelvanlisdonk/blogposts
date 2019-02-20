---
ID: 848
post_title: >
  Get first day of current week or last
  week with TSQL
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/12/14/get-first-day-of-current-week-or-last-week-with-tsql/
published: true
post_date: 2009-12-14 16:01:38
---
To get the first day of the current week use:
<pre class="code"><span style="color: blue;">select </span><span style="color: magenta;">dateadd</span><span style="color: gray;">(</span>dd<span style="color: gray;">, (</span><span style="color: magenta;">datepart</span><span style="color: gray;">(</span>dw<span style="color: gray;">, </span><span style="color: magenta;">getdate</span><span style="color: gray;">()) * -</span>1<span style="color: gray;">) + </span>2<span style="color: gray;">, </span><span style="color: magenta;">getdate</span><span style="color: gray;">())</span></pre>
To get the first day of previous week and last day of previous week use:
<pre class="code"><span style="color: blue;">select </span><span style="color: magenta;">dateadd</span><span style="color: gray;">(</span><span style="color: magenta;">day</span><span style="color: gray;">, -</span>8<span style="color: gray;">, </span><span style="color: magenta;">dateadd</span><span style="color: gray;">(</span>dd<span style="color: gray;">, (</span><span style="color: magenta;">datepart</span><span style="color: gray;">(</span>dw<span style="color: gray;">, </span><span style="color: magenta;">getdate</span><span style="color: gray;">()) * -</span>1<span style="color: gray;">) + </span>2<span style="color: gray;">, </span><span style="color: magenta;">getdate</span><span style="color: gray;">()))
</span><span style="color: blue;">select </span><span style="color: magenta;">dateadd</span><span style="color: gray;">(</span><span style="color: magenta;">day</span><span style="color: gray;">, -</span>1<span style="color: gray;">, </span><span style="color: magenta;">dateadd</span><span style="color: gray;">(</span>dd<span style="color: gray;">, (</span><span style="color: magenta;">datepart</span><span style="color: gray;">(</span>dw<span style="color: gray;">, </span><span style="color: magenta;">getdate</span><span style="color: gray;">()) * -</span>1<span style="color: gray;">) + </span>2<span style="color: gray;">, </span><span style="color: magenta;">getdate</span><span style="color: gray;">()))</span></pre>
You can also, use a variable for the current date and time, like:
<pre class="code"><span style="color: blue;">declare </span>@currentDateTime <span style="color: blue;">as datetime
set </span>@currentDateTime <span style="color: gray;">= </span><span style="color: red;">'2011-01-15 07:47:31.887' 

</span><span style="color: blue;">select </span><span style="color: magenta;">dateadd</span><span style="color: gray;">(</span><span style="color: magenta;">day</span><span style="color: gray;">, -</span>8<span style="color: gray;">, </span><span style="color: magenta;">dateadd</span><span style="color: gray;">(</span>dd<span style="color: gray;">, (</span><span style="color: magenta;">datepart</span><span style="color: gray;">(</span>dw<span style="color: gray;">, </span>@currentDateTime<span style="color: gray;">) * -</span>1<span style="color: gray;">) + </span>2<span style="color: gray;">, </span>@currentDateTime<span style="color: gray;">))
</span><span style="color: green;">-- Result: 2011-01-02 07:47:31.887

</span><span style="color: blue;">select </span><span style="color: magenta;">dateadd</span><span style="color: gray;">(</span><span style="color: magenta;">day</span><span style="color: gray;">, -</span>1<span style="color: gray;">, </span><span style="color: magenta;">dateadd</span><span style="color: gray;">(</span>dd<span style="color: gray;">, (</span><span style="color: magenta;">datepart</span><span style="color: gray;">(</span>dw<span style="color: gray;">, </span>@currentDateTime<span style="color: gray;">) * -</span>1<span style="color: gray;">) + </span>2<span style="color: gray;">, </span>@currentDateTime<span style="color: gray;">))
</span><span style="color: green;">-- Result: 2011-01-09 07:47:31.887</span></pre>
---
ID: 3671
post_title: >
  How to get the day of week of a all
  dates between start and end date in
  T-SQL
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/01/22/how-to-get-the-day-of-week-of-a-all-dates-between-start-and-end-date-in-t-sql/
published: true
post_date: 2014-01-22 16:19:56
---
<p>If you want to get a list of all dates between a start and end date and their corresponding day of week in T-SQL, you can use the following code:</p>  <pre class="code"><span style="color: blue">set datefirst </span>1

<span style="color: blue">declare </span><span style="color: teal">@StartDate </span><span style="color: blue">date </span><span style="color: gray">= </span><span style="color: red">'2014-01-20'
</span><span style="color: blue">declare </span><span style="color: teal">@EndDate </span><span style="color: blue">date </span><span style="color: gray">= </span><span style="color: red">'2014-01-27'


</span><span style="color: gray">;</span><span style="color: blue">with </span><span style="color: teal">cte </span><span style="color: gray">(</span><span style="color: teal">dt</span><span style="color: gray">, </span><span style="color: teal">dw</span><span style="color: gray">) </span><span style="color: blue">as
</span><span style="color: gray">(
  </span><span style="color: blue">select </span><span style="color: magenta">cast</span><span style="color: gray">(</span><span style="color: teal">@StartDate </span><span style="color: blue">as date</span><span style="color: gray">), </span><span style="color: magenta">datepart</span><span style="color: gray">(</span><span style="color: teal">dw</span><span style="color: gray">, </span><span style="color: teal">@StartDate</span><span style="color: gray">)
  </span><span style="color: blue">union </span><span style="color: gray">all
  </span><span style="color: blue">select </span><span style="color: magenta">dateadd</span><span style="color: gray">(</span><span style="color: magenta">day</span><span style="color: gray">, </span>1<span style="color: gray">, </span><span style="color: teal">dt</span><span style="color: gray">), </span><span style="color: magenta">datepart</span><span style="color: gray">(</span><span style="color: teal">dw</span><span style="color: gray">, </span><span style="color: magenta">dateadd</span><span style="color: gray">(</span><span style="color: magenta">day</span><span style="color: gray">, </span>1<span style="color: gray">, </span><span style="color: teal">dt</span><span style="color: gray">))
  </span><span style="color: blue">from </span><span style="color: teal">cte
  </span><span style="color: blue">where </span><span style="color: magenta">dateadd</span><span style="color: gray">(</span><span style="color: magenta">day</span><span style="color: gray">, </span>1<span style="color: gray">, </span><span style="color: teal">dt</span><span style="color: gray">) &lt;= </span><span style="color: teal">@EndDate
</span><span style="color: gray">)
</span><span style="color: blue">select </span><span style="color: teal">dt</span><span style="color: gray">, </span><span style="color: teal">dw
</span><span style="color: blue">from </span><span style="color: teal">cte
</span></pre>

<p><strong>Result</strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/01/image11.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/01/image_thumb11.png" width="220" height="275" /></a></p>
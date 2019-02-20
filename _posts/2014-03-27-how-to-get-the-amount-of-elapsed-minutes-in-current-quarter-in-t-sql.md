---
ID: 3708
post_title: >
  How to get the amount of elapsed minutes
  in current quarter in T-SQL
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/03/27/how-to-get-the-amount-of-elapsed-minutes-in-current-quarter-in-t-sql/
published: true
post_date: 2014-03-27 11:05:19
---
<p>If you want to know the amount of elapsed minutes in the current quarter, you can use the following T-SQL code:</p>  <pre class="code"><span style="background: white; color: blue">declare </span><span style="background: white; color: black">@CurrentDateTime </span><span style="background: white; color: blue">datetime </span><span style="background: white; color: gray">= </span><span style="background: white; color: red">'2014-03-27 10:56:10'
</span><span style="background: white; color: blue">declare </span><span style="background: white; color: black">@MinutesPassedInHour </span><span style="background: white; color: blue">int </span><span style="background: white; color: gray">= </span><span style="background: white; color: magenta">convert</span><span style="background: white; color: gray">(</span><span style="background: white; color: blue">int</span><span style="background: white; color: gray">, </span><span style="background: white; color: magenta">datepart</span><span style="background: white; color: gray">(</span><span style="background: white; color: magenta">minute</span><span style="background: white; color: gray">, </span><span style="background: white; color: black">@CurrentDateTime</span><span style="background: white; color: gray">))
</span><span style="background: white; color: blue">declare </span><span style="background: white; color: black">@quarterCount </span><span style="background: white; color: blue">int </span><span style="background: white; color: gray">= </span><span style="background: white; color: black">@MinutesPassedInHour </span><span style="background: white; color: gray">/ </span><span style="background: white; color: black">15
</span><span style="background: white; color: blue">declare </span><span style="background: white; color: black">@MinutesPassedInQuarter </span><span style="background: white; color: blue">int </span><span style="background: white; color: gray">= (</span><span style="background: white; color: black">@MinutesPassedInHour </span><span style="background: white; color: gray">- (</span><span style="background: white; color: black">@quarterCount </span><span style="background: white; color: gray">* </span><span style="background: white; color: black">15</span><span style="background: white; color: gray">))
</span><span style="background: white; color: blue">select </span><span style="background: white; color: black">@MinutesPassedInQuarter

</span><span style="background: white; color: green">-- Result: 11</span></pre>
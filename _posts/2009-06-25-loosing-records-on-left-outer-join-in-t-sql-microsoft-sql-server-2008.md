---
ID: 579
post_title: >
  Loosing records on left outer join in
  T-SQL Microsoft SQL Server 2008
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/06/25/loosing-records-on-left-outer-join-in-t-sql-microsoft-sql-server-2008/
published: true
post_date: 2009-06-25 10:13:33
---
<p>If you do a left outer join and you loose records of the “left” table, this might be caused by the where clause:   <br />    <br />This query will result in all records of table Production.HourGroup, only Production.HourGroup rows that have a correspoding Production.SortPerHour and on Production.SortPerHour.Sortday ‘2009-04-21’ are counted.    <br /></p>  <pre class="code"><span style="color: blue">select
    </span>u<span style="color: gray">.</span>HourGroup   <span style="color: gray">,
    </span><span style="color: magenta">sum</span><span style="color: gray">(</span><span style="color: magenta">isnull</span><span style="color: gray">(</span>s.Amount<span style="color: gray">,</span>0<span style="color: gray">))
</span><span style="color: blue">from
    </span>Production<span style="color: gray">.</span>HourGroup u
<span style="color: gray">left outer join
    </span>Production<span style="color: gray">.</span>SortPerHour s <span style="color: blue">on </span>u<span style="color: gray">.</span>HourGroup <span style="color: gray">= </span>s<span style="color: gray">.</span>HourGroup <span style="color: gray">and </span>s<span style="color: gray">.</span>Sortday <span style="color: gray">=  </span><span style="color: red">'2009-04-21'
</span><span style="color: blue">group by </span>u<span style="color: gray">.</span>HourGroup
<span style="color: blue">order by </span>u<span style="color: gray">.</span>HourGroup</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>
  <br />But the query below will not result in all records of table Production.HourGroup, because of the where clause.

  <br />The where clause is run on the left outer join result. So only the records in table Production.HourGroup with a corresponding SortPerHour on Sortday ‘2009-01-21’ will be listed and counted.

  <br /></p>

<pre class="code"><span style="color: blue">select
    </span>u<span style="color: gray">.</span>HourGroup   <span style="color: gray">,
    </span><span style="color: magenta">sum</span><span style="color: gray">(</span><span style="color: magenta">isnull</span><span style="color: gray">(</span>s<span style="color: gray">.</span>Amount<span style="color: gray">,</span>0<span style="color: gray">))
</span><span style="color: blue">from
    </span>Production<span style="color: gray">.</span>HourGroup u
<span style="color: gray">left outer join
    </span>Production<span style="color: gray">.</span>SortPerHour s <span style="color: blue">on </span>u<span style="color: gray">.</span>HourGroup <span style="color: gray">= </span>s<span style="color: gray">.</span>HourGroup
<span style="color: blue">where
    </span>s<span style="color: gray">.</span>Sortday <span style="color: gray">= </span><span style="color: red">'2009-04-21'
</span><span style="color: blue">group by </span>u<span style="color: gray">.</span>HourGroup
<span style="color: blue">order by </span>u<span style="color: gray">.</span>HourGroup</pre>
<a href="http://11011.net/software/vspaste"></a><a href="http://11011.net/software/vspaste"></a>
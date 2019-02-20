---
ID: 2779
post_title: 'How to convert / cast the current server date and time to a varchar in the format YYYY-MM-DDThh:mm:ss[+|-]hh:mm in T-SQL'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/08/13/how-to-convert-cast-the-current-server-date-and-time-to-a-varchar-in-the-format-yyyy-mm-ddthhmmss-hhmm-in-t-sql/
published: true
post_date: 2012-08-13 15:26:00
---
<p>&#160;</p>  <p>To convert the current machine date and time to a varchar in the format YYYY-MM-DDThh:mm:ss[+|-]hh:mm in T-SQL, you can use the following code:</p>  <pre class="code"><p><span style="color: blue"></span>&#160;</p><p><span style="color: blue">select </span><span style="color: magenta">convert</span><span style="color: gray">(</span><span style="color: blue">varchar</span><span style="color: gray">(</span>100<span style="color: gray">), </span><span style="color: magenta">cast</span><span style="color: gray">(</span><span style="color: magenta">sysdatetimeoffset</span><span style="color: gray">() </span><span style="color: blue">as datetimeoffset</span><span style="color: gray">(</span>0<span style="color: gray">)), </span>126<span style="color: gray">)
</span></p></pre>


<p>&#160;</p>

<p><strong>Result (in Amsterdam in Summer time)</strong></p>

<p>2012-08-13T15:23:09+02:00</p>
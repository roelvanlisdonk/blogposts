---
ID: 756
post_title: 'Measure execution time in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/10/15/measure-execution-time-in-c/
published: true
post_date: 2009-10-15 16:16:40
---
<p>To measure execution time in C#, substract start and end datetime.   <br /></p>  <pre class="code"><span style="color: blue">         public void </span>MeasureTime()
        {

            <span style="color: green">// Capture start time
            </span><span style="color: #2b91af">DateTime </span>startDateTime = <span style="color: #2b91af">DateTime</span>.Now;

            <span style="color: green">// Do something for 1000ms...
            </span><span style="color: #2b91af">Thread</span>.Sleep(1000);

            <span style="color: green">// Capture end time
            </span><span style="color: #2b91af">DateTime </span>endDateTime = <span style="color: #2b91af">DateTime</span>.Now;

            <span style="color: green">// Determine duration
            </span><span style="color: #2b91af">TimeSpan </span>duration = endDateTime - startDateTime;

            <span style="color: green">// Show duration
            </span><span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;Hours{0} Minutes{1} Seconds {2}, Milliseconds{3}&quot;</span>,duration.Hours, duration.Minutes, duration.Seconds,duration.Milliseconds));
        }</pre>
<a href="http://11011.net/software/vspaste"></a>
---
ID: 1240
post_title: 'How to convert a text containing a datetime in format &ldquo;yyyyMMdd_HHmmss&rdquo; to a datetime in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/04/16/how-to-convert-a-text-containing-a-datetime-in-format-yyyymmdd_hhmmss-to-a-datetime-in-c/
published: true
post_date: 2010-04-16 10:20:43
---
<p>If you want to convert a text containing a datetime in format “yyyyMMdd_HHmmss” to a datetime vaiable in C#, use the following code:</p>  <p>&#160;</p>  <p><strong>UnitTest</strong></p>  <pre class="code"><span style="color: blue">string </span>dateTimeFormat = <span style="color: #a31515">&quot;yyyyMMdd_HHmmss&quot;</span>;
<span style="color: blue">string </span>textContainingDateTime = <span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;This is some text containing a datetime 20100808_080808 in the format [{0}]&quot;</span>, dateTimeFormat);
<span style="color: #2b91af">DateTime </span>result = <span style="color: #2b91af">DateTime</span>.Now;
<span style="color: #2b91af">DateTime</span>.TryParseExact(textContainingDateTime.Substring(40, dateTimeFormat.Length), dateTimeFormat, System.Globalization.<span style="color: #2b91af">CultureInfo</span>.InvariantCulture, System.Globalization.<span style="color: #2b91af">DateTimeStyles</span>.None, <span style="color: blue">out </span>result);
<span style="color: #2b91af">DateTime </span>expectedResult = <span style="color: blue">new </span><span style="color: #2b91af">DateTime</span>(2010,8,8,8,8,8);
<span style="color: #2b91af">Assert</span>.AreEqual(expectedResult, result);</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p><strong>Result</strong></p>

<p>Passed</p>
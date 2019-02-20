---
ID: 2976
post_title: >
  Convert a date object to a string in
  JavaScript
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/11/30/convert-a-date-object-to-a-string-in-javascript/
published: true
post_date: 2012-11-30 09:50:00
---
<p>If you want to convert a date object to a string in JavaScript and you use jQuery, then you can use the function <strong>$.datepicker.formatDate.</strong></p>  <p>&#160;</p>  <p>The following QUnit test will succeed:</p>  <pre class="code"><span style="background: white; color: green">/// &lt;reference path=&quot;Scripts/qunit.js&quot;/&gt;
/// &lt;reference path=&quot;Scripts/jquery-1.8.3.js&quot;/&gt;
/// &lt;reference path=&quot;Scripts/jquery-ui-1.9.2.js&quot;/&gt;
</span><span style="background: white; color: #a31515">&quot;use strict&quot;</span><span style="background: white; color: black">;

test(</span><span style="background: white; color: #a31515">'JsTest'</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
{
    
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">input = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">Date(2012, 10, 28); </span><span style="background: white; color: green">// Note: months start at zero!
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">expected = </span><span style="background: white; color: #a31515">'2012-11-28'</span><span style="background: white; color: black">;
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">actual = $.datepicker.formatDate(</span><span style="background: white; color: #a31515">'yy-mm-dd'</span><span style="background: white; color: black">, input);
    ok(expected == actual,
        </span><span style="background: white; color: #a31515">'Dates are not equal. Expected:' </span><span style="background: white; color: black">+
        expected + </span><span style="background: white; color: #a31515">' _ Actual:' </span><span style="background: white; color: black">+ actual);
});</span></pre>
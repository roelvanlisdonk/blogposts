---
ID: 2973
post_title: Convert string to date in JavaScript
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/11/30/convert-string-to-date-in-javascript/
published: true
post_date: 2012-11-30 09:40:36
---
<p>If you want to convert a string to a date object in JavaScript and you use jQuery, then you can use the function <strong>$.datepicker.parseDate.</strong> </p>  <p>&#160;</p>  <p>The following QUnit test will succeed:</p>   <pre class="code"><span style="background: white; color: green">/// &lt;reference path=&quot;Scripts/qunit.js&quot;/&gt;
/// &lt;reference path=&quot;Scripts/jquery-1.8.3.js&quot;/&gt;
/// &lt;reference path=&quot;Scripts/jquery-ui-1.9.2.js&quot;/&gt;
</span><span style="background: white; color: #a31515">&quot;use strict&quot;</span><span style="background: white; color: black">;

test(</span><span style="background: white; color: #a31515">'JsTest'</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
{
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">text = </span><span style="background: white; color: #a31515">'2012-11-28'</span><span style="background: white; color: black">;
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">expected = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">Date(2012, 10, 28); </span><span style="background: white; color: green">// Note: months start at zero!
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">actual = $.datepicker.parseDate(</span><span style="background: white; color: #a31515">'yy-mm-dd'</span><span style="background: white; color: black">, text);
    ok(expected.getTime() == actual.getTime(),
        </span><span style="background: white; color: #a31515">'Dates are not equal. Expected:' </span><span style="background: white; color: black">+
        expected.toISOString() + </span><span style="background: white; color: #a31515">' _ Actual:' </span><span style="background: white; color: black">+ actual.toISOString());
});</span></pre>
---
ID: 557
post_title: 'Convert dutch string  to DateTime and DateTime to dutch String with TryParseExact in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/06/18/convert-dutch-string-to-datetime-and-datetime-to-dutch-string-with-tryparseexact-in-c/
published: true
post_date: 2009-06-18 10:36:54
---
<p>To convert a dutch string to DateTime and a DateTime to a dutch string in C# use the class:   <br /></p>  <pre class="code"><span style="color: blue">    public class </span><span style="color: #2b91af">DateTimeHelper
    </span>{
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Returns a DateTime object if conversion from dutch string succeeded.
        </span><span style="color: gray">/// </span><span style="color: green">Return DateTime.MinValue if conversion from dutch string failed.
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;dateTime&quot;&gt;</span><span style="color: green">The string to convert</span><span style="color: gray">&lt;/param&gt;
        /// &lt;returns&gt;</span><span style="color: green">See description</span><span style="color: gray">&lt;/returns&gt;
        </span><span style="color: blue">public </span><span style="color: #2b91af">DateTime </span>ConvertDutchStringToDateTime(<span style="color: blue">string </span>dateTime)
        {
            <span style="color: #2b91af">DateTime </span>result = <span style="color: #2b91af">DateTime</span>.MinValue;
            <span style="color: blue">bool </span>conversionResult = <span style="color: #2b91af">DateTime</span>.TryParseExact(dateTime, <span style="color: #a31515">&quot;dd-MM-yyyy&quot;</span>, <span style="color: #2b91af">CultureInfo</span>.InvariantCulture, <span style="color: #2b91af">DateTimeStyles</span>.None, <span style="color: blue">out  </span>result);
            <span style="color: blue">return </span>result;
        }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Return a dutch datetime formatted string.
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;dateTime&quot;&gt;</span><span style="color: green">DateTime object to convert</span><span style="color: gray">&lt;/param&gt;
        /// &lt;returns&gt;</span><span style="color: green">See description</span><span style="color: gray">&lt;/returns&gt;
        </span><span style="color: blue">public string </span>ConvertDateTimeToDutchString(<span style="color: #2b91af">DateTime </span>dateTime)
        {
            <span style="color: blue">return </span>dateTime.ToString(<span style="color: #a31515">&quot;dd-MM-yyyy&quot;</span>);
        }
    }</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>
  <br /><strong>UnitTest class
    <br /></strong></p>

<pre class="code">    [<span style="color: #2b91af">TestFixture</span>]
    <span style="color: blue">public class </span><span style="color: #2b91af">DateTimeHelperTest
    </span>{
        [<span style="color: #2b91af">Test</span>]
        <span style="color: blue">public void </span>ConvertDutchStringToDateTime_Basic()
        {
            <span style="color: #2b91af">DateTimeHelper </span>helper = <span style="color: blue">new </span><span style="color: #2b91af">DateTimeHelper</span>();
            <span style="color: #2b91af">DateTime </span>dateTime = helper.ConvertDutchStringToDateTime(<span style="color: #a31515">&quot;12-01-2009&quot;</span>);
            <span style="color: #2b91af">Assert</span>.That(dateTime, <span style="color: #2b91af">Is</span>.EqualTo(<span style="color: blue">new </span><span style="color: #2b91af">DateTime</span>(2009,1,12)));
        }
        [<span style="color: #2b91af">Test</span>]
        <span style="color: blue">public void </span>ConvertDateTimeToDutchString_Basic()
        {
            <span style="color: #2b91af">DateTimeHelper </span>helper = <span style="color: blue">new </span><span style="color: #2b91af">DateTimeHelper</span>();
            <span style="color: blue">string </span>result = helper.ConvertDateTimeToDutchString(<span style="color: blue">new </span><span style="color: #2b91af">DateTime</span>(2009, 1, 12));
            <span style="color: #2b91af">Assert</span>.That(result, <span style="color: #2b91af">Is</span>.EqualTo(<span style="color: #a31515">&quot;12-01-2009&quot;</span>));
        }
    }</pre>
<a href="http://11011.net/software/vspaste"></a>
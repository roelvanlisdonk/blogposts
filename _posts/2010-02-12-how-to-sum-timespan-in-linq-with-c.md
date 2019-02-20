---
ID: 1032
post_title: 'How to sum TimeSpan in LINQ with C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/02/12/how-to-sum-timespan-in-linq-with-c/
published: true
post_date: 2010-02-12 11:47:47
---
<p>If you want to sum TimeSpan properties in LINQ with C#, use:</p>  <pre class="code"><span style="color: #2b91af">            List</span>&lt;<span style="color: #2b91af">TimeSpan</span>&gt; list = <span style="color: blue">new </span><span style="color: #2b91af">List</span>&lt;<span style="color: #2b91af">TimeSpan</span>&gt;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; {
                <span style="color: blue">new </span><span style="color: #2b91af">TimeSpan</span>(1),
                <span style="color: blue">new </span><span style="color: #2b91af">TimeSpan</span>(2),
                <span style="color: blue">new </span><span style="color: #2b91af">TimeSpan</span>(3)
            };

            <span style="color: green">// TimeSpan.Zero is the initial offset, in this case 0 ticks
            // subtotal is used to sum to items in the list
            // t is the current item in the list
            </span><span style="color: #2b91af">TimeSpan </span>total = list.Aggregate(<span style="color: #2b91af">TimeSpan</span>.Zero, (subtotal, t) =&gt; subtotal.Add(t));

            <span style="color: #2b91af">Console</span>.WriteLine(total.Ticks);

            <span style="color: green">// Result: 6</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p>&#160;</p>

<p><a href="http://11011.net/software/vspaste"></a></p>

<p>Thanks to: <a title="http://stackoverflow.com/questions/970178/c-how-to-use-the-enumerable-aggregate-method" href="http://stackoverflow.com/questions/970178/c-how-to-use-the-enumerable-aggregate-method">http://stackoverflow.com/questions/970178/c-how-to-use-the-enumerable-aggregate-method</a></p>
---
ID: 850
post_title: 'Uppercase first letter of a string in C# (C sharp)'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/12/15/uppercase-first-letter-of-a-string-in-c-c-sharp/
published: true
post_date: 2009-12-15 07:59:57
---
<p>To uppercase the first letter of a string in C#, use:</p>  <pre class="code"><span style="color: gray">        /// &lt;summary&gt;
        /// </span><span style="color: green">Capatilize first word in string
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;s&quot;&gt;&lt;/param&gt;
        /// &lt;returns&gt;&lt;/returns&gt;
        </span><span style="color: blue">public string </span>UppercaseFirst(<span style="color: blue">string </span>s)
        {
            <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(s))
            {
                <span style="color: blue">return string</span>.Empty;
            }
            <span style="color: blue">char</span>[] a = s.ToCharArray();
            a[0] = <span style="color: blue">char</span>.ToUpper(a[0]);

            <span style="color: blue">return new string</span>(a);
        }</pre>
<a href="http://11011.net/software/vspaste"></a>
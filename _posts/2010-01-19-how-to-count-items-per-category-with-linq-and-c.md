---
ID: 989
post_title: 'How to count items per category with LINQ and C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/01/19/how-to-count-items-per-category-with-linq-and-c/
published: true
post_date: 2010-01-19 08:57:07
---
<p>If you want to count items per category with LINQ in C#, you van use:</p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Text;
<span style="color: blue">using </span>NUnit.Framework;
<span style="color: blue">using </span>NUnit.Framework.SyntaxHelpers;

<span style="color: blue">namespace </span>Ada.Cdf.Test
{
  [<span style="color: #2b91af">TestFixture</span>]
  <span style="color: blue">public class </span><span style="color: #2b91af">IntegrationTester
  </span>{
    [<span style="color: #2b91af">Test</span>]
    [<span style="color: #2b91af">Explicit</span>(<span style="color: #a31515">&quot;Not a unittest&quot;</span>)]
    <span style="color: blue">public void </span>Test()
    {
      <span style="color: #2b91af">List</span>&lt;<span style="color: blue">string</span>&gt; items = <span style="color: blue">new </span><span style="color: #2b91af">List</span>&lt;<span style="color: blue">string</span>&gt;();
      items.Add(<span style="color: #a31515">&quot;Item 1&quot;</span>);
      items.Add(<span style="color: #a31515">&quot;Item 2&quot;</span>);
      items.Add(<span style="color: #a31515">&quot;Item 3&quot;</span>);
      items.Add(<span style="color: #a31515">&quot;Item 4&quot;</span>);
      items.Add(<span style="color: #a31515">&quot;Item 2&quot;</span>);
      items.Add(<span style="color: #a31515">&quot;Item 3&quot;</span>);

      <span style="color: blue">var </span>result = <span style="color: blue">from </span>i <span style="color: blue">in </span>items
                   <span style="color: blue">group </span>i <span style="color: blue">by </span>i <span style="color: blue">into </span>g
                   <span style="color: blue">select new </span>{Group=g.Key, ItemCount= g.Count()};

      <span style="color: blue">foreach </span>(<span style="color: blue">var </span>test <span style="color: blue">in </span>result)
      {
        <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;Group[{0}] ItemCount[{1}]&quot;</span>, test.Group, test.ItemCount));
      }
    }
  }
}</pre>

<p>&#160;</p>

<p>Result</p>

<p>Group[Item 1] ItemCount[1]
  <br />Group[Item 2] ItemCount[2]

  <br />Group[Item 3] ItemCount[2]

  <br />Group[Item 4] ItemCount[1] </p>

<p>&#160;</p>

<p><a href="http://11011.net/software/vspaste">&#160;</a></p>
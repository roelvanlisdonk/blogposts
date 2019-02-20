---
ID: 988
post_title: 'Get index of an item with LINQ and C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/01/19/get-index-of-an-item-with-linq-and-c/
published: true
post_date: 2010-01-19 08:48:08
---
<p>If you want to use the index of an item with LINQ in C#, you can use the “index” statement:</p>  <pre class="code"><span style="color: blue">using </span>System;
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

      <span style="color: blue">var </span>result = items.Select((item, index) =&gt; <span style="color: blue">new </span>{ index, item });
                   <span style="color: green">//select new { Name=i, Ind=index };
      </span><span style="color: blue">foreach </span>(<span style="color: blue">var </span>test <span style="color: blue">in </span>result)
      {
        <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;item[{0}] index[{1}]&quot;</span>, test.item, test.index));
      }

    }
  }
}</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>
  <br />

  <br />Result</p>

<p>item[Item 1] index[0]
  <br />item[Item 2] index[1]

  <br />item[Item 3] index[2]

  <br />item[Item 4] index[3]

  <br />item[Item 2] index[4]

  <br />item[Item 3] index[5] </p>

<p>1 passed, 0 failed, 0 skipped, took 2,81 seconds (NUnit 2.4).</p>
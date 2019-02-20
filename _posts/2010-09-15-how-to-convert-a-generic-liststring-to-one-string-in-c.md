---
ID: 1722
post_title: 'How to convert a generic List&lt;string&gt; to one string and back in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/09/15/how-to-convert-a-generic-liststring-to-one-string-in-c/
published: true
post_date: 2010-09-15 12:57:36
---
<p>If you want to concatenate all items in a generic List&lt;string&gt; in C# you can use the following code:</p>  <p>&#160;</p>  <pre class="code"><span style="color: #2b91af">List</span>&lt;<span style="color: blue">string</span>&gt; itemsInGenericList = <span style="color: blue">new </span><span style="color: #2b91af">List</span>&lt;<span style="color: blue">string</span>&gt;
    {
    <span style="color: #a31515">&quot;Item 1&quot;</span>,
    <span style="color: #a31515">&quot;Item 2&quot;</span>,
    <span style="color: #a31515">&quot;Item 3&quot;</span>,
    <span style="color: #a31515">&quot;Item 4&quot;
    </span>};

<span style="color: green">// Convert generic list of strings to an array of strings.
</span><span style="color: blue">string</span>[] itemsInArray = itemsInGenericList.ToArray();

<span style="color: green">// Convert an array of strings to one string.
</span><span style="color: blue">string </span>itemsInString = <span style="color: blue">string</span>.Join(<span style="color: #2b91af">Environment</span>.NewLine, itemsInArray);
<span style="color: #2b91af">Console</span>.WriteLine(itemsInString);

<span style="color: green">// Convert an array of strings to a generic list of strings.
</span>itemsInGenericList = <span style="color: blue">new </span><span style="color: #2b91af">List</span>&lt;<span style="color: blue">string</span>&gt;(itemsInArray);</pre>


<p>&#160;</p>

<p><strong>Result</strong></p>

<p>Item 1
  <br />

  <br />Item 2</p>

<p>Item 3</p>

<p>Item 4</p>
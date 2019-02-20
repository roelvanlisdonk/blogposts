---
ID: 2332
post_title: 'How to pass an object of an anonymous type to a function in C#, by using the dynamic keyword.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/01/04/how-to-pass-an-object-of-an-anonymous-type-to-a-function-in-c-by-using-the-dynamic-keyword/
published: true
post_date: 2012-01-04 16:44:09
---
<p>If you are using LINQ and create a new anonymous type, this object can be passed to a function by using a parameter of type object. But if you, want to use the properties a more cleaner approach would be using the dynamic keyword in C#:</p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Dynamic;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>Microsoft.CSharp;</pre>


<pre class="code">[<span style="color: #2b91af">TestMethod</span>]
<span style="color: blue">public void </span>Test()
{
    PassingObjectsOfAnAnonymousTypeToAFunction();   
}
<span style="color: blue">public void </span>PassingObjectsOfAnAnonymousTypeToAFunction()
{
    <span style="color: green">// Create a list of names.
    </span><span style="color: #2b91af">List</span>&lt;<span style="color: blue">string</span>&gt; names = <span style="color: blue">new </span><span style="color: #2b91af">List</span>&lt;<span style="color: blue">string</span>&gt;();
    names.Add(<span style="color: #a31515">&quot;Name_1&quot;</span>);
    names.Add(<span style="color: #a31515">&quot;Name_2&quot;</span>);
    names.Add(<span style="color: #a31515">&quot;Name_20&quot;</span>);
    names.Add(<span style="color: #a31515">&quot;Name_3&quot;</span>);

    <span style="color: green">// Filter names.
    </span><span style="color: blue">var </span>query = <span style="color: blue">from </span>n <span style="color: blue">in </span>names
                <span style="color: blue">where </span>n.Contains(<span style="color: #a31515">&quot;2&quot;</span>)
                <span style="color: blue">select new </span>{ Name = n, MyExtraProperty = <span style="color: #a31515">&quot;Added some extra property&quot; </span>};
    <span style="color: blue">var </span>filteredItems = query.ToList();

    <span style="color: green">// Write filtered names to console.
    </span><span style="color: blue">foreach </span>(<span style="color: blue">var </span>fi <span style="color: blue">in </span>filteredItems)
    {
        FunctionWithAnonymouseParameters(fi);
    }
}
<span style="color: blue">public void </span>FunctionWithAnonymouseParameters(<span style="color: blue">dynamic </span>name)
{
    <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;Name=[{0}] MyExtraProperty=[{1}]&quot;</span>, name.Name, name.MyExtraProperty));
}</pre>


<h2>Result</h2>

<p>&#160;</p>

<p>Name=[Name_2] MyExtraProperty=[Added some extra property]
  <br />Name=[Name_20] MyExtraProperty=[Added some extra property]</p>
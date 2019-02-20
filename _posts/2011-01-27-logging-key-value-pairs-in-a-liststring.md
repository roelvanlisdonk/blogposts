---
ID: 1892
post_title: 'Logging key value pairs in a List&lt;string&gt;'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/01/27/logging-key-value-pairs-in-a-liststring/
published: true
post_date: 2011-01-27 13:11:25
---
<p>If you have a List&lt;string&gt; with entries:</p>  <p>[0] = Parameter1.Name</p>  <p>[1] = Parameter1.Value</p>  <p>[2] = Parameter2.Name</p>  <p>[3] = Parameter2.Value</p>  <p>and want to convert this list to a string like Parameter1.Name = [Parameter1.Value] Parameter2.Name = [Parameter2.Value], you can use the following code:</p>  <p>&#160;</p>  <pre class="code"><span style="color: gray">/// &lt;summary&gt;
/// </span><span style="color: green">Convert a List of strings to a string in the format: Variable1.Name = [Variabel1.Value] Variable2.Name = [Variabel2.Value]
</span><span style="color: gray">/// &lt;/summary&gt;
/// &lt;param name=&quot;variables&quot;&gt;
/// </span><span style="color: green">Can't be null
</span><span style="color: gray">/// </span><span style="color: green">Should have an evennumber of items
</span><span style="color: gray">/// &lt;/param&gt;
/// &lt;returns&gt;&lt;/returns&gt;
</span><span style="color: blue">public static string </span>GetFormattedLine(<span style="color: #2b91af">List</span>&lt;<span style="color: blue">string</span>&gt; variables)
{
    <span style="color: #2b91af">StringBuilder </span>result = <span style="color: blue">new </span><span style="color: #2b91af">StringBuilder</span>(<span style="color: blue">string</span>.Empty);

    <span style="color: blue">if </span>(variables == <span style="color: blue">null</span>)
    {
        <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentException</span>(<span style="color: #2b91af">“Can't be null”</span>, <span style="color: #a31515">&quot;variables&quot;</span>);
    }

    <span style="color: blue">if </span>(variables.Count % 2 != 0)
    {
        <span style="color: blue">throw new </span><span style="color: #2b91af">ApplicationException</span>(<span style="color: blue">string</span>.Format(<span style="color: #2b91af">“[{0}] is not an evennumber”</span>, <span style="color: #a31515">&quot;variabels.Count&quot;</span>));
    }

    <span style="color: blue">for </span>(<span style="color: blue">int </span>i = 0; i &lt; variables.Count; i++)
    {
        <span style="color: blue">if </span>(i % 2 == 0)
        {
            result.AppendFormat(<span style="color: #a31515">&quot;{0} = [{1}] &quot;</span>, variables[i], variables[i + 1]);   
        }
    }

    <span style="color: blue">return </span>result.ToString().Trim();
}</pre>
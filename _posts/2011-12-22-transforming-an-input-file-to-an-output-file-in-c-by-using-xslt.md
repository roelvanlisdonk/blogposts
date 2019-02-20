---
ID: 2315
post_title: 'Transforming an input file to an output file in C#, by using XSLT.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/12/22/transforming-an-input-file-to-an-output-file-in-c-by-using-xslt/
published: true
post_date: 2011-12-22 10:04:31
---
<p>Just a code snippet for transforming an input file to an output file in C# by using XSLT:</p>   <pre class="code"><span style="color: gray">/// &lt;summary&gt;
/// </span><span style="color: green">Transform an input file to an output file, by using XSLT.
</span><span style="color: gray">/// &lt;/summary&gt;
</span><span style="color: blue">public void </span>ExecuteTransform()
{
    <span style="color: blue">string </span>xsltFilePath = <span style="color: #a31515">@&quot;C:\BDATA\Transform.xsl&quot;</span>;
    <span style="color: blue">string </span>sourceFilePath = <span style="color: #a31515">@&quot;C:\BDATA\input.xml&quot;</span>;
    <span style="color: blue">string </span>destinationFilePath = <span style="color: #a31515">@&quot;C:\BDATA\output.xml&quot;</span>;

    <span style="color: blue">var </span>transform = <span style="color: blue">new </span><span style="color: #2b91af">XslCompiledTransform</span>();
    transform.Load(xsltFilePath);
    transform.Transform(sourceFilePath, destinationFilePath);
}</pre>
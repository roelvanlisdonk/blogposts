---
ID: 2463
post_title: >
  How to convert a XML file based on
  attributes to an XML file based on child
  nodes by using XSLT.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/01/20/how-to-convert-a-xml-file-based-on-attributes-to-an-xml-file-based-on-child-nodes-by-using-xslt/
published: true
post_date: 2012-01-20 14:59:09
---
<p>I wanted to convert a XML based on attributes to a XML based on child nodes, e.g.:</p>  <p>&#160;</p>  <p><strong>Input</strong></p>  <pre class="code"><p><span style="color: blue">&lt;?</span><span style="color: #a31515">xml </span><span style="color: red">version</span><span style="color: blue">=</span>&quot;<span style="color: blue">1.0</span>&quot; <span style="color: red">encoding</span><span style="color: blue">=</span>&quot;<span style="color: blue">utf-8</span>&quot; <span style="color: blue">?&gt; 
&lt;</span><span style="color: #a31515">people</span><span style="color: blue">&gt;
  &lt;</span><span style="color: #a31515">person </span><span style="color: red">firstname</span><span style="color: blue">=</span>&quot;<span style="color: blue">John</span>&quot; <span style="color: red">lastname</span><span style="color: blue">=</span>&quot;<span style="color: blue">Smith</span>&quot;<span style="color: blue">/&gt;
  &lt;</span><span style="color: #a31515">person </span><span style="color: red">firstname</span><span style="color: blue">=</span>&quot;<span style="color: blue">Michael</span>&quot; <span style="color: red">lastname</span><span style="color: blue">=</span>&quot;<span style="color: blue">Johnson</span>&quot;<span style="color: blue">/&gt;
  &lt;</span><span style="color: #a31515">person </span><span style="color: red">firstname</span><span style="color: blue">=</span>&quot;<span style="color: blue">Jacob</span>&quot; <span style="color: red">lastname</span><span style="color: blue">=</span>&quot;<span style="color: blue">Williams</span>&quot;<span style="color: blue">/&gt;
&lt;/</span><span style="color: #a31515">people</span><span style="color: blue">&gt;</span></p></pre>


<p><strong>Output</strong></p>

<pre class="code"><span style="color: blue">&lt;</span><span style="color: #a31515">people</span><span style="color: blue">&gt;
  &lt;</span><span style="color: #a31515">person</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">firstname</span><span style="color: blue">&gt;</span>John<span style="color: blue">&lt;/</span><span style="color: #a31515">firstname</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">lastname</span><span style="color: blue">&gt;</span>Smith<span style="color: blue">&lt;/</span><span style="color: #a31515">lastname</span><span style="color: blue">&gt;
  &lt;/</span><span style="color: #a31515">person</span><span style="color: blue">&gt;
  &lt;</span><span style="color: #a31515">person</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">firstname</span><span style="color: blue">&gt;</span>Michael<span style="color: blue">&lt;/</span><span style="color: #a31515">firstname</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">lastname</span><span style="color: blue">&gt;</span>Johnson<span style="color: blue">&lt;/</span><span style="color: #a31515">lastname</span><span style="color: blue">&gt;
  &lt;/</span><span style="color: #a31515">person</span><span style="color: blue">&gt;
  &lt;</span><span style="color: #a31515">person</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">firstname</span><span style="color: blue">&gt;</span>Jacob<span style="color: blue">&lt;/</span><span style="color: #a31515">firstname</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">lastname</span><span style="color: blue">&gt;</span>Williams<span style="color: blue">&lt;/</span><span style="color: #a31515">lastname</span><span style="color: blue">&gt;
  &lt;/</span><span style="color: #a31515">person</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">people</span><span style="color: blue">&gt;</span></pre>

<p><strong>XSLT</strong></p>

<p>The forum post [<a href="http://stackoverflow.com/questions/6496334/c-sharp-to-convert-xml-attributes-to-elements">http://stackoverflow.com/questions/6496334/c-sharp-to-convert-xml-attributes-to-elements</a>] contains a XSLT script that will just do that.</p>

<pre class="code"><span style="color: blue">&lt;</span><span style="color: #2b91af">xsl:stylesheet </span><span style="color: red">version</span><span style="color: blue">=</span>&quot;<span style="color: blue">1.0</span>&quot;
 <span style="color: red">xmlns:xsl</span><span style="color: blue">=</span>&quot;<span style="color: blue">http://www.w3.org/1999/XSL/Transform</span>&quot;
 <span style="color: red">xmlns:x</span><span style="color: blue">=</span>&quot;<span style="color: blue">http://www.something.com</span>&quot;<span style="color: blue">&gt;
  &lt;</span><span style="color: #2b91af">xsl:output </span><span style="color: red">omit-xml-declaration</span><span style="color: blue">=</span>&quot;<span style="color: blue">yes</span>&quot; <span style="color: red">indent</span><span style="color: blue">=</span>&quot;<span style="color: blue">yes</span>&quot;<span style="color: blue">/&gt;
  &lt;</span><span style="color: #2b91af">xsl:strip-space </span><span style="color: red">elements</span><span style="color: blue">=</span>&quot;<span style="color: blue">*</span>&quot;<span style="color: blue">/&gt;

  &lt;</span><span style="color: #2b91af">xsl:variable </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">vNamespace</span>&quot; <span style="color: red">select</span><span style="color: blue">=</span>&quot;<span style="color: blue">namespace-uri(/*)</span>&quot;<span style="color: blue">/&gt;

  &lt;</span><span style="color: #2b91af">xsl:template </span><span style="color: red">match</span><span style="color: blue">=</span>&quot;<span style="color: blue">node()|@*</span>&quot;<span style="color: blue">&gt;
    &lt;</span><span style="color: #2b91af">xsl:copy</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #2b91af">xsl:apply-templates </span><span style="color: red">select</span><span style="color: blue">=</span>&quot;<span style="color: blue">node()|@*</span>&quot;<span style="color: blue">/&gt;
    &lt;/</span><span style="color: #2b91af">xsl:copy</span><span style="color: blue">&gt;
  &lt;/</span><span style="color: #2b91af">xsl:template</span><span style="color: blue">&gt;

  &lt;</span><span style="color: #2b91af">xsl:template </span><span style="color: red">match</span><span style="color: blue">=</span>&quot;<span style="color: blue">*/*/@*</span>&quot;<span style="color: blue">&gt;
    &lt;</span><span style="color: #2b91af">xsl:element </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">{name()}</span>&quot; <span style="color: red">namespace</span><span style="color: blue">=</span>&quot;<span style="color: blue">{$vNamespace}</span>&quot;<span style="color: blue">&gt;
      &lt;</span><span style="color: #2b91af">xsl:value-of </span><span style="color: red">select</span><span style="color: blue">=</span>&quot;<span style="color: blue">.</span>&quot;<span style="color: blue">/&gt;
    &lt;/</span><span style="color: #2b91af">xsl:element</span><span style="color: blue">&gt;
  &lt;/</span><span style="color: #2b91af">xsl:template</span><span style="color: blue">&gt;

  &lt;</span><span style="color: #2b91af">xsl:template </span><span style="color: red">match</span><span style="color: blue">=</span>&quot;<span style="color: blue">x:Value</span>&quot;<span style="color: blue">&gt;
    &lt;</span><span style="color: #2b91af">xsl:copy</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #2b91af">xsl:apply-templates</span><span style="color: blue">/&gt;
    &lt;/</span><span style="color: #2b91af">xsl:copy</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #2b91af">xsl:apply-templates </span><span style="color: red">select</span><span style="color: blue">=</span>&quot;<span style="color: blue">@*</span>&quot;<span style="color: blue">/&gt;
  &lt;/</span><span style="color: #2b91af">xsl:template</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #2b91af">xsl:stylesheet</span><span style="color: blue">&gt;
</span></pre>
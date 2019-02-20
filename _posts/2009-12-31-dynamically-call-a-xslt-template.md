---
ID: 901
post_title: Dynamically call a xslt template
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/12/31/dynamically-call-a-xslt-template/
published: true
post_date: 2009-12-31 11:43:11
---
<p>You cannot call a xslt template like:</p>  <pre class="code"><span style="color: blue">&lt;</span><span style="color: #2b91af">xsl:variable </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<font color="#0000ff">templateName</font>&quot; <span style="color: red">select</span><span style="color: blue">=</span>&quot;test&quot;<span style="color: blue">&gt;&lt;/</span><span style="color: #2b91af">xsl:variable</span><span style="color: blue">&gt;</span></pre>

<pre class="code"><span style="color: blue">&lt;</span><span style="color: #2b91af">xsl:call-template </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">$<font color="#0000ff">templateName</font></span>&quot;<span style="color: blue">&gt;</span></pre>
<a href="http://11011.net/software/vspaste"></a><a href="http://11011.net/software/vspaste"></a>

<pre class="code"><span style="color: blue">&lt;</span><span style="color: #2b91af">xsl:template </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<font color="#0000ff">test</font>&quot;<span style="color: blue">&gt;
</span><span style="color: blue">&lt;/</span><span style="color: #2b91af">xsl:template</span><span style="color: blue">&gt;</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>
  <br />The clossed you can get to calling a xslt template dynamically is to use the &lt;xsl:if or &lt;xsl:choose based on a variable:</p>

<pre class="code"><span style="color: blue">&lt;</span><span style="color: #2b91af">xsl:if </span><span style="color: red">test</span><span style="color: blue">=</span>&quot;$parameter1=<span style="color: blue">$<font color="#0000ff">templateName</font></span>&quot;<span style="color: blue">&gt;
</span><span style="color: blue">  <span style="color: blue">&lt;</span><span style="color: #2b91af">xsl:call-template </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<font color="#0000ff">test</font>&quot;<span style="color: blue">&gt;<br /></span></span><span style="color: blue">&lt;/</span><span style="color: #2b91af">xsl:if</span><span style="color: blue">&gt;</span></pre>
<a href="http://11011.net/software/vspaste"></a><a href="http://11011.net/software/vspaste"></a>
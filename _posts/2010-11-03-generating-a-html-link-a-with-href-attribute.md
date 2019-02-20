---
ID: 1791
post_title: 'Generating a HTML link &lt;A&gt;, with href attribute'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/11/03/generating-a-html-link-a-with-href-attribute/
published: true
post_date: 2010-11-03 14:40:39
---
<p>There are 2 ways to generate a HTML &lt;A&gt; link with XSLT:</p>  <p>&#160;</p>  <p><strong>Using the &lt;xsl:element&gt;</strong></p>  <pre class="code">        <span style="color: blue">&lt;</span><span style="color: #2b91af">xsl:element </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">a</span>&quot;<span style="color: blue">&gt;
            &lt;</span><span style="color: #2b91af">xsl:attribute </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">href</span>&quot;<span style="color: blue">&gt;
                &lt;</span><span style="color: #2b91af">xsl:value-of </span><span style="color: red">select</span><span style="color: blue">=</span>&quot;u<span style="color: blue">rl</span>&quot;<span style="color: blue">/&gt;
            &lt;/</span><span style="color: #2b91af">xsl:attribute</span><span style="color: blue">&gt;
            &lt;</span><span style="color: #2b91af">xsl:value-of </span><span style="color: red">select</span><span style="color: blue">=</span>&quot;u<span style="color: blue">rl</span>&quot;<span style="color: blue">/&gt;
        &lt;/</span><span style="color: #2b91af">xsl:element</span><span style="color: blue">&gt;
</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p><strong>Using only text</strong></p>

<pre class="code"><span style="color: blue">&lt;</span><span style="color: #a31515">a </span><span style="color: red">href</span><span style="color: blue">=</span>&quot;<span style="color: blue">{url}</span>&quot;<span style="color: blue">&gt;&lt;</span><span style="color: #2b91af">xsl:value-of </span><span style="color: red">select</span><span style="color: blue">=</span>&quot;<span style="color: blue">url</span>&quot;<span style="color: blue">/&gt;&lt;/</span><span style="color: #a31515">a</span><span style="color: blue">&gt;
</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p><strong>HTML link, that fires a JavaScript function with parameter</strong></p>

<pre class="code"><span style="color: blue">&lt;</span><span style="color: #2b91af">xsl:element </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">a</span>&quot;<span style="color: blue">&gt;
   &lt;</span><span style="color: #2b91af">xsl:attribute </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">href</span>&quot;<span style="color: blue">&gt;</span>javascript:myFunction(<span style="color: blue">&lt;</span><span style="color: #2b91af">xsl:value-of </span><span style="color: red">select</span><span style="color: blue">=</span>&quot;<span style="color: blue">@parameter1</span>&quot;<span style="color: blue">/&gt;</span>);<span style="color: blue">&lt;/</span><span style="color: #2b91af">xsl:attribute</span><span style="color: blue">&gt;
      </span>My link text
<span style="color: blue">&lt;/</span><span style="color: #2b91af">xsl:element</span><span style="color: blue">&gt;
</span></pre>
<a href="http://11011.net/software/vspaste"></a>
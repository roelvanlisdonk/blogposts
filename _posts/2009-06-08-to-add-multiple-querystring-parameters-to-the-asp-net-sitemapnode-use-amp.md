---
ID: 517
post_title: 'To add multiple QueryString parameters to the ASP .NET SiteMapNode use &amp;'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/06/08/to-add-multiple-querystring-parameters-to-the-asp-net-sitemapnode-use-amp/
published: true
post_date: 2009-06-08 16:30:28
---
To add multiple QueryString parameters to the ASP .NET SiteMapNode use &amp;amp;  <br />  <br />  <br />  <pre class="code"><span style="color: blue">&lt;?</span><span style="color: #a31515">xml </span><span style="color: red">version</span><span style="color: blue">=</span>&quot;<span style="color: blue">1.0</span>&quot; <span style="color: red">encoding</span><span style="color: blue">=</span>&quot;<span style="color: blue">utf-8</span>&quot; <span style="color: blue">?&gt;
&lt;</span><span style="color: #a31515">siteMap </span><span style="color: red">xmlns</span><span style="color: blue">=</span>&quot;<span style="color: blue">http://schemas.microsoft.com/AspNet/SiteMap-File-1.0</span>&quot; <span style="color: blue">&gt;
  &lt;</span><span style="color: #a31515">siteMapNode </span><span style="color: red">title</span><span style="color: blue">=</span>&quot;<span style="color: blue">Home</span>&quot; <span style="color: red">description</span><span style="color: blue">=</span>&quot;<span style="color: blue">Home</span>&quot; <span style="color: red">url</span><span style="color: blue">=</span>&quot;<span style="color: blue">Default.aspx</span>&quot; <span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">siteMapNode </span><span style="color: red">title</span><span style="color: blue">=</span>&quot;<span style="color: blue">Test Rapport</span>&quot; <span style="color: red">description</span><span style="color: blue">=</span>&quot;<span style="color: blue">Test Rapport</span>&quot;
     <span style="color: red">url</span><span style="color: blue">=</span>&quot;<span style="color: blue">~/Rapporten/ViewReport.aspx?rapport=test</span><span style="color: red">&amp;amp;</span><span style="color: blue">productId=1</span>&quot; <span style="color: blue">/&gt;</span><span style="color: blue">
  &lt;/</span><span style="color: #a31515">siteMapNode</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">siteMap</span><span style="color: blue">&gt;</span></pre>
<a href="http://11011.net/software/vspaste"></a>
---
ID: 1788
post_title: 'Setting the default document for you&rsquo;re ASP .NET website or webservice, by using the Web.config'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/10/31/setting-the-default-document-for-youre-asp-net-website-or-webservice-by-using-the-web-config/
published: true
post_date: 2010-10-31 20:46:44
---
<p>If you want to set the default document for you’re ASP .NET website or WCF webservice, you can use the Web.config. Add the following XML to you’re Web.config just before the end tag: &lt;/configuration&gt;</p>  <pre class="code"><p> <span style="color: blue">&lt;</span><span style="color: #a31515">system.webServer</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">defaultDocument</span><span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">files</span><span style="color: blue">&gt;
                &lt;</span><span style="color: #a31515">add </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">MyWcfService.svc</span>&quot; <span style="color: blue">/&gt;
            &lt;/</span><span style="color: #a31515">files</span><span style="color: blue">&gt;
        &lt;/</span><span style="color: #a31515">defaultDocument</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">system.webServer</span><span style="color: blue">&gt;
</span></p><p><span style="color: blue"></span>&#160;</p><p><span style="color: blue"></span>&#160;</p></pre>
<a href="http://11011.net/software/vspaste"></a>
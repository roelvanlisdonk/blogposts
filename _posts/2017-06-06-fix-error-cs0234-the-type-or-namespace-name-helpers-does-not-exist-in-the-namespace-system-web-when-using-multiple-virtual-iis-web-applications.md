---
ID: 5079
post_title: 'Fix: error CS0234: The type or namespace name &#8216;Helpers&#8217; does not exist in the namespace &#8216;System.Web&#8217;, when using multiple virtual IIS web applications'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2017/06/06/fix-error-cs0234-the-type-or-namespace-name-helpers-does-not-exist-in-the-namespace-system-web-when-using-multiple-virtual-iis-web-applications/
published: true
post_date: 2017-06-06 10:21:54
---
<p><font size="2">I have a ASP .NET 4.5.2 MVC web application running on an IIS website and I wanted to run a separate ASP .NET 4.5.2. web api application under the MVC web site. </font></p>  <p><font size="2">Both projects worked just fine, when hosting them as separate IIS websites, but when the web api was “mounted” as virtual web application under the MVC website I was getting the errors below, when hitting the web api application:</font></p>  <p><font size="2"></font></p>  <pre>error CS0234: The type or namespace name 'Helpers' does not exist in the namespace 'System.Web' (are you missing an assembly reference?)</pre>

<p><font size="2"></font></p>

<pre>error CS0234: The type or namespace name 'Mvc' does not exist in the namespace 'System.Web' (are you missing an assembly reference?)</pre>

<p><code></code></p>
<code>
  <pre>Line 150:    &lt;pages controlRenderingCompatibilityVersion=&quot;4.0&quot;&gt;
Line 151:      &lt;namespaces&gt;
Line 152:        &lt;add namespace=&quot;System.Web.Helpers&quot; /&gt;
Line 153:        &lt;add namespace=&quot;System.Web.Mvc&quot; /&gt;
Line 154:        &lt;add namespace=&quot;System.Web.Mvc.Ajax&quot; /&gt;</pre>
</code>



<p><font size="2">So I was hitting the web api, but got an error on the parent MVC web application???</font></p>

<p><font size="2"></font></p>

<p><font size="2">Turns out, I had to remove these namespaces in the web api web.config, because those dll’s are not in the web api project.</font></p>

<p><font size="2"></font></p>

<p><font size="2">Adding the following lines to the web.config of the web api project, solved the errors.</font></p>

<p><font size="1">&lt;configuration&gt;</font></p>

<p><font size="1">&lt;system.web&gt;</font></p>

<p><font size="1">&lt;pages controlRenderingCompatibilityVersion=&quot;4.0&quot;&gt;
    <br />&#160;&#160;&#160;&#160;&#160; &lt;namespaces&gt;

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &lt;clear/&gt;

    <br />&#160;&#160;&#160;&#160;&#160; &lt;/namespaces&gt;

    <br />&#160;&#160;&#160; &lt;/pages&gt;</font></p>

<p><font size="1"></font></p>

<p><font size="1">…</font></p>

<p><font size="2"></font></p>

<p><font size="2"></font></p>

<p><font size="2"></font></p>
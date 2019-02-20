---
ID: 1734
post_title: 'Solving the error: The debugger&rsquo;s protocol is incompatible with the debuggee in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/09/20/solving-the-error-the-debuggers-protocol-is-incompatible-with-the-debuggee-in-c/
published: true
post_date: 2010-09-20 10:57:25
---
<p>When you get the error: Error while trying to run project: ‘C:\…’</p>  <p>The debugger’s protocol is incompatible with the debuggee</p>  <p>Check you’re supportedRuntime tag in you’re App.config or Web.config</p>  <p>I ported a .NET 4.0 C# application back to .NET 3.5 and got that message, removing the startup tag:</p>  <pre class="code"><span style="color: blue">&lt;</span><span style="color: #a31515">startup</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">supportedRuntime </span><span style="color: red">version</span><span style="color: blue">=</span>&quot;<span style="color: blue">v4.0</span>&quot; <span style="color: red">sku</span><span style="color: blue">=</span>&quot;<span style="color: blue">.NETFramework,Version=v4.0</span>&quot;<span style="color: blue">/&gt;
  &lt;/</span><span style="color: #a31515">startup</span><span style="color: blue">&gt;</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>Solved the problem</p>

<p>&#160;</p>

<p><strong>Screendump</strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/09/image3.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/09/image_thumb3.png" width="754" height="107" /></a></p>
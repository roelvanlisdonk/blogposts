---
ID: 3748
post_title: 'Solving: Found conflicts between different versions of the same dependent assembly.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/04/28/solving-found-conflicts-between-different-versions-of-the-same-dependent-assembly/
published: true
post_date: 2014-04-28 13:49:10
---
<p>&#160;</p>  <p>I was getting the warning: C:\Windows\Microsoft.NET\Framework\v4.0.30319\Microsoft.Common.targets(1546,5): warning MSB3247: Found conflicts between different versions of the same dependent assembly.</p>  <p>The was caused by the referenced assembly System.Net.Http. </p>  <p><strong>Solution</strong></p>  <p>Edit the *.csproj file and change: </p>  <p>&lt;Reference Include=&quot;System.Net.Http, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL&quot; /&gt;</p>  <p>to</p>  <p>&lt;Reference Include=&quot;System.Net.Http, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL&quot; /&gt;</p>  <p>&#160;</p>  <p><a title="http://connect.microsoft.com/VisualStudio/feedback/details/733213/warning-generated-for-default-asp-net-mvc-4-project" href="http://connect.microsoft.com/VisualStudio/feedback/details/733213/warning-generated-for-default-asp-net-mvc-4-project">http://connect.microsoft.com/VisualStudio/feedback/details/733213/warning-generated-for-default-asp-net-mvc-4-project</a></p>  <p>&#160;</p>  <p>&#160;</p>  <p>And in the web.config add:</p>  <pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: #a31515">runtime</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: #a31515">assemblyBinding </span><span style="background: white; color: red">xmlns</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">urn:schemas-microsoft-com:asm.v1</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">&gt;
     </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: #a31515">dependentAssembly</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: #a31515">assemblyIdentity </span><span style="background: white; color: red">name</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">System.Net.Http</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">culture</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">neutral</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">publicKeyToken</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">b03f5f7f11d50a3a</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: blue">/&gt;
        &lt;</span><span style="background: white; color: #a31515">bindingRedirect </span><span style="background: white; color: red">oldVersion</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">0.0.0.0-4.0.0.0</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">newVersion</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">4.0.0.0</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: blue">/&gt;
      &lt;/</span><span style="background: white; color: #a31515">dependentAssembly</span><span style="background: white; color: blue">&gt;</span></pre>
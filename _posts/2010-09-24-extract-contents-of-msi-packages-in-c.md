---
ID: 1741
post_title: 'Extract contents of msi packages in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/09/24/extract-contents-of-msi-packages-in-c/
published: true
post_date: 2010-09-24 15:30:55
---
<p>If you want to extract the contents of a msi package to filesystem, you can use the following C# function:</p>  <p>&#160;</p>  <pre class="code"><p><span style="color: blue">public void </span>ExtractMsiPackage()
   {&#160;&#160;&#160; <span style="color: blue">string </span>parameters = <span style="color: blue">string</span>.Empty;
       parameters = <span style="color: blue">string</span>.Format(<span style="color: #a31515">@&quot;/a {0} /qb TARGETDIR=&quot;&quot;{1}&quot;&quot; REINSTALLMODE=amus&quot;</span>, </p><p>       &quot;C:\Temp\Test.msi&quot;, &quot;C:\Temp\Extract&quot;);
       <span style="color: #2b91af">Process </span>process = <span style="color: #2b91af">Process</span>.Start(<span style="color: #a31515">&quot;msiexec&quot;</span>, parameters);
       process.WaitForExit();
   }</p></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>/a = Administrative mode</p>

<p>/qb = Minimal UI, UI will only display progressbar</p>

<p>TARGETDIR = Folder to extract the contents to</p>

<p>REINSTALLMODE = amus, will overwrite all existing files and registry settings</p>
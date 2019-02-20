---
ID: 3585
post_title: >
  How to get the absolute root folder path
  of a ASP .NET website / MVC website.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/11/20/how-to-get-the-absolute-root-folder-path-of-a-asp-net-website-mvc-website/
published: true
post_date: 2013-11-20 16:13:39
---
<p>&#160;</p>  <p>The following code result in my case to rootFolderPath = &quot;C:\inetpub\wwwroot\MvcApplication1&quot;.</p>  <pre class="code"><span style="background: white; color: #2b91af">Uri </span><span style="background: white; color: black">uri = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">System.</span><span style="background: white; color: #2b91af">Uri</span><span style="background: white; color: black">(</span><span style="background: white; color: #2b91af">Assembly</span><span style="background: white; color: black">.GetAssembly(</span><span style="background: white; color: blue">typeof</span><span style="background: white; color: black">(</span><span style="background: white; color: #2b91af">MvcApplication</span><span style="background: white; color: black">)).CodeBase);
</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">binFolderPath = </span><span style="background: white; color: #2b91af">Path</span><span style="background: white; color: black">.GetDirectoryName(uri.LocalPath);
</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">rootFolderPath = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">DirectoryInfo</span><span style="background: white; color: black">(binFolderPath).Parent.FullName;</span></pre>
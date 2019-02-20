---
ID: 1879
post_title: >
  Cleaning a Microsoft Visual Studio
  solution after setting all files to
  read-only
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/01/17/cleaning-a-microsoft-visual-studio-solution-after-setting-all-files-to-read-only/
published: true
post_date: 2011-01-17 14:56:11
---
<p>Making &quot;.\bin&quot;, &quot;.\Release&quot;, &quot;.\Debug&quot;, &quot;.\obj&quot; not read-only, after accidentally setting the root folder of you’re Microsoft Visual Studio solution to &quot;read-only&quot;.</p>  <p>You can use this script:</p>  <p>&#160;</p>  <p>&#160;</p>  <pre class="code"><p><span style="color: blue">string </span>sourceFolder = <span style="color: #a31515">@&quot;C:\Projects&quot;</span>;
<span style="color: blue">foreach </span>(<span style="color: blue">string </span>folder <span style="color: blue">in </span><span style="color: #2b91af">Directory</span>.GetDirectories(sourceFolder, <span style="color: #a31515">&quot;*&quot;</span>, SearchOption.AllDirectories))
{
<span style="color: blue">    if </span>(folder.EndsWith(<span style="color: #a31515">@&quot;\obj&quot;</span>) || folder.EndsWith(<span style="color: #a31515">@&quot;\bin&quot;</span>) || folder.EndsWith(<span style="color: #a31515">@&quot;\Release&quot;</span>) || folder.EndsWith(<span style="color: #a31515">@&quot;\Debug&quot;</span>))&#160;&#160;&#160;&#160; {&#160;&#160;&#160;&#160;&#160;&#160; <span style="color: #2b91af">DirectoryInfo </span>test = <span style="color: blue">new </span><span style="color: #2b91af">DirectoryInfo</span>(folder);&#160;&#160;&#160;&#160;&#160;&#160; test.Attributes = FileAttributes.Normal;</p><p>&#160;&#160;&#160;&#160;&#160;&#160; <span style="color: blue">foreach</span>(<span style="color: #2b91af">DirectoryInfo </span>dir <span style="color: blue">in </span>test.GetDirectories(<span style="color: #a31515">&quot;*&quot;</span>, SearchOption.AllDirectories))&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; {</p><p>&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; dir.Attributes = FileAttributes.Normal;</p><p>&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; }</p><p>
                    
<span style="color: blue">        foreach </span>(<span style="color: blue">string </span>file <span style="color: blue">in </span><span style="color: #2b91af">Directory</span>.GetFiles(folder, <span style="color: #a31515">&quot;*&quot;</span>, SearchOption.AllDirectories))&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; {
<span style="color: #2b91af">          File</span>.SetAttributes(file, FileAttributes.Normal);
<span style="color: #2b91af">          File</span>.Delete(file);&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; }</p><p>
      }
}
</p></pre>
---
ID: 1738
post_title: 'Find and Replace text in all files of a given folder , including subfolders with C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/09/24/find-and-replace-text-in-all-files-of-a-given-folder-including-subfolders-with-c/
published: true
post_date: 2010-09-24 11:27:07
---
<p>If you want to find and replace some text in all files of a given folder, including subfolders, you can use the following C# code:</p>  <pre class="code"><span style="color: blue">   string </span>rootfolder = <span style="color: #a31515">@&quot;C:\Temp&quot;</span>;
   <span style="color: blue">string</span>[] files = <span style="color: #2b91af">Directory</span>.GetFiles(rootfolder, <span style="color: #a31515">&quot;*.*&quot;</span>, <span style="color: #2b91af">SearchOption</span>.AllDirectories);
   <span style="color: blue">foreach </span>(<span style="color: blue">string </span>file <span style="color: blue">in </span>files)
   {&#160;&#160;&#160; <span style="color: blue">try
     </span>{&#160;&#160;&#160; <span style="color: blue">string </span>contents = <span style="color: #2b91af">File</span>.ReadAllText(file);
       contents = contents.Replace(<span style="color: #a31515">@&quot;Text to find&quot;</span>, <span style="color: #a31515">@&quot;Replacement text&quot;</span>);</pre>

<pre class="code"><span style="color: green">       // Make files writable
       </span><span style="color: #2b91af">File</span>.SetAttributes(file, <span style="color: #2b91af">FileAttributes</span>.Normal);</pre>
<a href="http://11011.net/software/vspaste"></a>

<pre class="code">
       <span style="color: #2b91af">File</span>.WriteAllText(file, contents);
     }
     <span style="color: blue">catch </span>(<span style="color: #2b91af">Exception </span>ex)
     {&#160;&#160;&#160; <span style="color: #2b91af">Console</span>.WriteLine(ex.Message);
     }
   }</pre>
<a href="http://11011.net/software/vspaste"></a>
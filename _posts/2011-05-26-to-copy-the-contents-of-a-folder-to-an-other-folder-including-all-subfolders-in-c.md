---
ID: 2070
post_title: 'To copy the contents of a folder to an other folder, including all subfolders in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/05/26/to-copy-the-contents-of-a-folder-to-an-other-folder-including-all-subfolders-in-c/
published: true
post_date: 2011-05-26 15:50:11
---
<p>To copy the contents of a folder to an other folder, including all subfolders, overwriting existing files, you can use the following function in C#:</p>  <p>&#160;</p>  <pre class="code"><span style="color: gray">/// &lt;summary&gt;
/// </span><span style="color: green">Copies the contents of a folder, including subfolders to an other folder, overwriting existing files
</span><span style="color: gray">/// &lt;/summary&gt;
/// &lt;param name=&quot;sourceFolder&quot;&gt;&lt;/param&gt;
/// &lt;param name=&quot;destinationFolder&quot;&gt;&lt;/param&gt;
</span><span style="color: blue">public static void </span>CopyFolderContents(<span style="color: blue">string </span>sourceFolder, <span style="color: blue">string </span>destinationFolder)
{
    <span style="color: blue">if </span>(<span style="color: #2b91af">Directory</span>.Exists(sourceFolder))
    {
        <span style="color: green">// Copy folder structure
        </span><span style="color: blue">foreach </span>(<span style="color: blue">string </span>sourceSubFolder <span style="color: blue">in </span><span style="color: #2b91af">Directory</span>.GetDirectories(sourceFolder, <span style="color: #a31515">&quot;*&quot;</span>, <span style="color: #2b91af">SearchOption</span>.AllDirectories))
        {
            <span style="color: #2b91af">Directory</span>.CreateDirectory(sourceSubFolder.Replace(sourceFolder, destinationFolder));
        }

        <span style="color: green">// Copy files
        </span><span style="color: blue">foreach </span>(<span style="color: blue">string </span>sourceFile <span style="color: blue">in </span><span style="color: #2b91af">Directory</span>.GetFiles(sourceFolder, <span style="color: #a31515">&quot;*&quot;</span>, <span style="color: #2b91af">SearchOption</span>.AllDirectories))
        {
            <span style="color: blue">string </span>destinationFile = sourceFile.Replace(sourceFolder, destinationFolder);
            <span style="color: #2b91af">File</span>.Copy(sourceFile, destinationFile, <span style="color: blue">true</span>);
        }
    }
}</pre>
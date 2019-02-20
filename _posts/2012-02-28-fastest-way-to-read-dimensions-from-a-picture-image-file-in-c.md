---
ID: 2511
post_title: 'Fastest way to read dimensions from a picture / image file in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/02/28/fastest-way-to-read-dimensions-from-a-picture-image-file-in-c/
published: true
post_date: 2012-02-28 17:36:20
---
<p>The fastest way to read the dimensions (width and height) from a picture / image file in C#, that I know of is:   <pre class="code"><span style="color: #2b91af">DateTime </span>startDateTime = <span style="color: #2b91af">DateTime</span>.Now;
<span style="color: blue">string </span>sourceFolder = <span style="color: #a31515">@&quot;C:\Temp&quot;</span>;

<span style="color: green">// Get all files from sourcefolder, including subfolders.
</span><span style="color: blue">string</span>[] sourceFiles = <span style="color: #2b91af">Directory</span>.GetFiles(sourceFolder, <span style="color: #a31515">&quot;*&quot;</span>, <span style="color: #2b91af">SearchOption</span>.AllDirectories);
<span style="color: blue">foreach </span>(<span style="color: blue">string </span>file <span style="color: blue">in </span>sourceFiles)
{
    <span style="color: blue">using </span>(<span style="color: #2b91af">Stream </span>stream = <span style="color: #2b91af">File</span>.OpenRead(file))
    {
        <span style="color: blue">using </span>(<span style="color: #2b91af">Image </span>sourceImage = <span style="color: #2b91af">Image</span>.FromStream(stream, <span style="color: blue">false</span>, <span style="color: blue">false</span>))
        {
            <span style="color: #2b91af">Console</span>.WriteLine(sourceImage.Width);
            <span style="color: #2b91af">Console</span>.WriteLine(sourceImage.Height);
        }
    }
}
<span style="color: #2b91af">DateTime </span>endDateTime = <span style="color: #2b91af">DateTime</span>.Now;

<span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Format(
    <span style="color: #a31515">&quot;Total duration [{0}] seconds. Total image count [{1}].&quot;</span>, 
    (endDateTime - startDateTime).TotalSeconds, 
    sourceFiles.Length));</pre>
  </p>


<p>Total duration <strong>[0,1855235] seconds</strong>. Total image count [33].</p>

<p>&#160;</p>

<p>This is like <strong>250x faster</strong>, then:

  <pre class="code"><span style="color: #2b91af">DateTime </span>startDateTime = <span style="color: #2b91af">DateTime</span>.Now;
<span style="color: blue">string </span>sourceFolder = <span style="color: #a31515">@&quot;C:\Temp&quot;</span>;

<span style="color: green">// Get all files from sourcefolder, including subfolders.
</span><span style="color: blue">string</span>[] sourceFiles = <span style="color: #2b91af">Directory</span>.GetFiles(sourceFolder, <span style="color: #a31515">&quot;*&quot;</span>, <span style="color: #2b91af">SearchOption</span>.AllDirectories);
<span style="color: blue">foreach </span>(<span style="color: blue">string </span>file <span style="color: blue">in </span>sourceFiles)
{
    <span style="color: blue">using </span>(<span style="color: #2b91af">Image </span>sourceImage = <span style="color: #2b91af">Image</span>.FromFile(file))
    {
        <span style="color: #2b91af">Console</span>.WriteLine(sourceImage.Width);
        <span style="color: #2b91af">Console</span>.WriteLine(sourceImage.Height);
    }
}
<span style="color: #2b91af">DateTime </span>endDateTime = <span style="color: #2b91af">DateTime</span>.Now;
<span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Format(
    <span style="color: #a31515">&quot;Total duration [{0}] seconds. Total image count [{1}].&quot;</span>, 
    (endDateTime - startDateTime).TotalSeconds, 
    sourceFiles.Length));</pre>
</p>

<p>Total duration <strong>[47,4575263] seconds</strong>. Total image count [33].</p>
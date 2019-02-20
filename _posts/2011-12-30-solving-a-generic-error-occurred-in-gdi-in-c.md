---
ID: 2326
post_title: 'Solving: A generic error occurred in GDI+. in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/12/30/solving-a-generic-error-occurred-in-gdi-in-c/
published: true
post_date: 2011-12-30 11:38:26
---
<p>I was creating an image in C# by using code similar to:</p>  <pre class="code"><span style="color: blue">public void </span>SaveImage()
{
    <span style="color: blue">byte</span>[] byteArray = <span style="color: blue">null</span>; <span style="color: green">// Put the bytes of the image here....

    </span><span style="color: #2b91af">Image </span>result = <span style="color: blue">null</span>;
    <span style="color: #2b91af">ImageFormat </span>format = <span style="color: #2b91af">ImageFormat</span>.Png;
    <span style="color: blue">using </span>(<span style="color: #2b91af">MemoryStream </span>ms = <span style="color: blue">new </span><span style="color: #2b91af">MemoryStream</span>(byteArray))
    {
        result = <span style="color: #2b91af">Image</span>.FromStream(ms);
    }

    <span style="color: blue">using </span>(<span style="color: #2b91af">Image </span>imageToExport = result)
    {
        <span style="color: blue">string </span>filePath = <span style="color: blue">string</span>.Format(<span style="color: #a31515">@&quot;C:\Temp\Myfile.{0}&quot;</span>, format.ToString());
        imageToExport.Save(filePath, format);
    }
}</pre>
This resulted in the error: &quot;A generic error occurred in GDI+.&quot; 

<p>&#160;</p>

<p>The error was resolved, after changing the code to:</p>

<pre class="code"><span style="color: blue">public void </span>SaveImage()
{
    <span style="color: blue">byte</span>[] byteArray = <span style="color: blue">null</span>; <span style="color: green">// Put the bytes of the image here....

    </span><span style="color: #2b91af">Image </span>result = <span style="color: blue">null</span>;
    <span style="color: #2b91af">ImageFormat </span>format = <span style="color: #2b91af">ImageFormat</span>.Png;
    <span style="color: blue"><pre class="code"><font color="#000000">  <font size="5">result = </font></font><font size="5"><span style="color: blue">new </span><span style="color: #2b91af">Bitmap</span>(<span style="color: blue">new </span><span style="color: #2b91af">MemoryStream</span><font color="#000000">(byteArray));</font></font>
</pre></span>
    <span style="color: blue">using </span>(<span style="color: #2b91af">Image </span>imageToExport = result)
    {
        <span style="color: blue">string </span>filePath = <span style="color: blue">string</span>.Format(<span style="color: #a31515">@&quot;C:\Temp\Myfile.{0}&quot;</span>, format.ToString());
        imageToExport.Save(filePath, format);
    }
}</pre>

<p>&#160;</p>

<p align="left">I found the solution at: <a href="http://stackoverflow.com/questions/1053052/a-generic-error-occurred-in-gdi-jpeg-image-to-memorystream">http://stackoverflow.com/questions/1053052/a-generic-error-occurred-in-gdi-jpeg-image-to-memorystream</a></p>
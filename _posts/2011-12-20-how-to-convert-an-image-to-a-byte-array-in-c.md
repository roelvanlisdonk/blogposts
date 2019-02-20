---
ID: 2307
post_title: 'How to: Convert an Image to a byte array in C#, by using a extension method.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/12/20/how-to-convert-an-image-to-a-byte-array-in-c/
published: true
post_date: 2011-12-20 16:34:14
---
<p>If you want to convert an Image to a byte array in C#, you can use the following extension method:</p>  <p>&#160;</p>  <pre class="code">[<span style="color: #2b91af">TestMethod</span>]
<span style="color: blue">public void </span>Test()
{
    <span style="color: #2b91af">Image </span>image = <span style="color: blue">null</span>; <span style="color: green">// Supply your image here.
    </span><span style="color: blue">byte</span>[] bytes = image.ToBytes();
}</pre>


<pre class="code"><span style="color: blue">using </span>System.Drawing;
<span style="color: blue">using </span>System.Drawing.Imaging;
<span style="color: blue">using </span>System.IO;

<span style="color: blue">namespace </span>Services.Extensions
{
    <span style="color: gray">/// &lt;summary&gt;
    /// </span><span style="color: green">Extensions to the [System.Drawing.Image] class
    </span><span style="color: gray">/// &lt;/summary&gt;
    </span><span style="color: blue">public static class </span><span style="color: #2b91af">ImageExtensions
    </span>{
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Converts an image to an array of bytes.
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;image&quot;&gt;</span><span style="color: green">The image.</span><span style="color: gray">&lt;/param&gt;
        /// &lt;returns&gt;&lt;/returns&gt;
        </span><span style="color: blue">public static byte</span>[] ToBytes(<span style="color: blue">this </span><span style="color: #2b91af">Image </span>image)
        {
            <span style="color: blue">byte</span>[] result = <span style="color: blue">null</span>;
            <span style="color: blue">using </span>(<span style="color: blue">var </span>stream = <span style="color: blue">new </span><span style="color: #2b91af">MemoryStream</span>())
            {
                image.Save(stream, image.RawFormat <span style="color: blue">as </span><span style="color: #2b91af">ImageFormat</span>);
                result = stream.ToArray();
            }
            <span style="color: blue">return </span>result;
        }
    }
}</pre>
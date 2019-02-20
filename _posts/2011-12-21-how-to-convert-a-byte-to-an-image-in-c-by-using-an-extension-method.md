---
ID: 2311
post_title: 'How to convert a byte[] to an image in C# by using an extension method.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/12/21/how-to-convert-a-byte-to-an-image-in-c-by-using-an-extension-method/
published: true
post_date: 2011-12-21 08:54:31
---
<p>To convert a byte array to an image in C#, you can use the following code:</p>  <pre class="code">[<span style="color: #2b91af">TestMethod</span>]
<span style="color: blue">public void </span>Test()
{
    <span style="color: blue">byte</span>[] bytes = <span style="color: blue">new byte</span>[100]; <span style="color: green">// Supply your bytes here. </span>
    <span style="color: #2b91af">Image </span>image = bytes.ToImage();
}</pre>

<pre class="code"><span style="color: blue">using </span>System.Drawing;
<span style="color: blue">using </span>System.IO;

<span style="color: blue">namespace </span>Services.Extensions
{
    <span style="color: gray">/// &lt;summary&gt;
    /// </span><span style="color: green">Contains extensions methods to the byte[] type.
    </span><span style="color: gray">/// &lt;/summary&gt;
    </span><span style="color: blue">public static class </span><span style="color: #2b91af">ByteArrayExtensions
    </span>{
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Creates an images, based on the given bytes.
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;image&quot;&gt;</span><span style="color: green">The image.</span><span style="color: gray">&lt;/param&gt;
        /// &lt;param name=&quot;byteArray&quot;&gt;</span><span style="color: green">The byte array.</span><span style="color: gray">&lt;/param&gt;
        /// &lt;returns&gt;&lt;/returns&gt;
        </span><span style="color: blue">public static </span><span style="color: #2b91af">Image </span>ToImage(<span style="color: blue">this byte</span>[] byteArray)
        {
            <span style="color: blue">return new </span><span style="color: #2b91af">Bitmap</span>(<span style="color: blue">new </span><span style="color: #2b91af">MemoryStream</span>(byteArray));
        }
    }
}</pre>
---
ID: 2559
post_title: 'How to convert a bitmap into a 1bpp monochrome TIFF in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/03/09/how-to-convert-a-bitmap-into-a-1bpp-monochrome-tiff-in-c/
published: true
post_date: 2012-03-09 10:38:37
---
<p>If you want to convert a bitmap into a TIFF, than then you can use the code:</p>  <pre class="code"><span style="color: blue">using </span>(System.Drawing.<span style="color: #2b91af">Bitmap </span>sourceBitmap = <span style="color: blue">new </span>System.Drawing.<span style="color: #2b91af">Bitmap</span>(<span style="color: #a31515">@&quot;C:\Temp\Source.bmp&quot;</span>))
{
    <span style="color: blue">string </span>outputFileName = <span style="color: #a31515">@&quot;C:\Temp\Destination.tiff&quot;</span>;
    <span style="color: blue">if </span>(System.IO.<span style="color: #2b91af">File</span>.Exists(outputFileName))
    {
        System.IO.<span style="color: #2b91af">File</span>.Delete(outputFileName);
    }
    sourceBitmap.Save(outputFileName, System.Drawing.Imaging.<span style="color: #2b91af">ImageFormat</span>.Tiff);
}</pre>

<p>If you want to convert a bitmap to a 1bpp monochrome TIFF in C#, I found 4 options:</p>

<p>1. <a href="http://www.bobpowell.net/onebit.htm">http://www.bobpowell.net/onebit.htm</a> ( no P-Invoke required, but not as fast as other methods )</p>

<p>2. <a href="http://social.msdn.microsoft.com/Forums/en/csharpgeneral/thread/9757dc94-11f3-4b30-a85c-cb9145eba12d">http://social.msdn.microsoft.com/Forums/en/csharpgeneral/thread/9757dc94-11f3-4b30-a85c-cb9145eba12d</a> (only when you are using WPF)</p>

<p>3. <a href="http://www.news2news.com/vfp/?example=493&amp;ver=vcs&amp;PHPSESSID=35494364de9987dfd2a9f3fe18f17565">http://www.news2news.com/vfp/?example=493&amp;ver=vcs&amp;PHPSESSID=35494364de9987dfd2a9f3fe18f17565</a> (less code then option 4, but did not have time to investigate)</p>

<p>4. <a href="http://www.wischik.com/lu/programmer/1bpp.html">http://www.wischik.com/lu/programmer/1bpp.html</a></p>

<p>&#160;</p>

<p>For the last options I cleanup some code:</p>

<pre class="code"><span style="color: blue">using </span>(System.Drawing.<span style="color: #2b91af">Bitmap </span>sourceBitmap = <span style="color: blue">new </span>System.Drawing.<span style="color: #2b91af">Bitmap</span>(<span style="color: #a31515">@&quot;C:\Temp\Source.bmp&quot;</span>))
{
    <span style="color: blue">using </span>(<span style="color: #2b91af">Bitmap </span>destinationBitmap = sourceBitmap.ConvertToMonochromeTiff())
    {
        <span style="color: blue">string </span>outputFileName = <span style="color: #a31515">@&quot;C:\Temp\Destination.tiff&quot;</span>;
        <span style="color: blue">if </span>(System.IO.<span style="color: #2b91af">File</span>.Exists(outputFileName))
        {
            System.IO.<span style="color: #2b91af">File</span>.Delete(outputFileName);
        }
        destinationBitmap.Save(outputFileName);
    }
}</pre>

<p>Where the ConvertToMonochromeTiff is an extension method to the System.Drawing.Bitmap type:</p>

<p>&#160;</p>

<pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Drawing;

<span style="color: blue">namespace </span>Rli.Extensions
{
    <span style="color: gray">/// &lt;summary&gt;
    /// </span><span style="color: green">Contains extensions methods to the System.Drawing.Bitmap type.
    </span><span style="color: gray">/// &lt;/summary&gt;
    </span><span style="color: blue">public static class </span><span style="color: #2b91af">BitmapExtensions
    </span>{
        <span style="color: blue">#region </span>P-Invoke
        [System.Runtime.InteropServices.<span style="color: #2b91af">DllImport</span>(<span style="color: #a31515">&quot;gdi32.dll&quot;</span>)]
        <span style="color: blue">public static extern bool </span>DeleteObject(IntPtr hObject);

        [System.Runtime.InteropServices.<span style="color: #2b91af">DllImport</span>(<span style="color: #a31515">&quot;user32.dll&quot;</span>)]
        <span style="color: blue">public static extern </span>IntPtr GetDC(IntPtr hwnd);

        [System.Runtime.InteropServices.<span style="color: #2b91af">DllImport</span>(<span style="color: #a31515">&quot;gdi32.dll&quot;</span>)]
        <span style="color: blue">public static extern </span>IntPtr CreateCompatibleDC(IntPtr hdc);

        [System.Runtime.InteropServices.<span style="color: #2b91af">DllImport</span>(<span style="color: #a31515">&quot;user32.dll&quot;</span>)]
        <span style="color: blue">public static extern int </span>ReleaseDC(IntPtr hwnd, IntPtr hdc);

        [System.Runtime.InteropServices.<span style="color: #2b91af">DllImport</span>(<span style="color: #a31515">&quot;gdi32.dll&quot;</span>)]
        <span style="color: blue">public static extern int </span>DeleteDC(IntPtr hdc);

        [System.Runtime.InteropServices.<span style="color: #2b91af">DllImport</span>(<span style="color: #a31515">&quot;gdi32.dll&quot;</span>)]
        <span style="color: blue">public static extern </span>IntPtr SelectObject(IntPtr hdc, IntPtr hgdiobj);

        [System.Runtime.InteropServices.<span style="color: #2b91af">DllImport</span>(<span style="color: #a31515">&quot;gdi32.dll&quot;</span>)]
        <span style="color: blue">public static extern int </span>BitBlt(IntPtr hdcDst, <span style="color: blue">int </span>xDst, <span style="color: blue">int </span>yDst, <span style="color: blue">int </span>w, <span style="color: blue">int </span>h, IntPtr hdcSrc, <span style="color: blue">int </span>xSrc, <span style="color: blue">int </span>ySrc, <span style="color: blue">int </span>rop);
        <span style="color: blue">static int </span>SRCCOPY = 0x00CC0020;

        [System.Runtime.InteropServices.<span style="color: #2b91af">DllImport</span>(<span style="color: #a31515">&quot;gdi32.dll&quot;</span>)]
        <span style="color: blue">static extern </span>IntPtr CreateDIBSection(IntPtr hdc, <span style="color: blue">ref </span>BITMAPINFO bmi, <span style="color: blue">uint </span>Usage, <span style="color: blue">out </span>IntPtr bits, IntPtr hSection, <span style="color: blue">uint </span>dwOffset);
        <span style="color: blue">static uint </span>BI_RGB = 0;
        <span style="color: blue">static uint </span>DIB_RGB_COLORS = 0;
        [System.Runtime.InteropServices.<span style="color: #2b91af">StructLayout</span>(System.Runtime.InteropServices.<span style="color: #2b91af">LayoutKind</span>.Sequential)]
        <span style="color: blue">public struct </span>BITMAPINFO
        {
            <span style="color: blue">public uint </span>biSize;
            <span style="color: blue">public int </span>biWidth, biHeight;
            <span style="color: blue">public short </span>biPlanes, biBitCount;
            <span style="color: blue">public uint </span>biCompression, biSizeImage;
            <span style="color: blue">public int </span>biXPelsPerMeter, biYPelsPerMeter;
            <span style="color: blue">public uint </span>biClrUsed, biClrImportant;
            [System.Runtime.InteropServices.<span style="color: #2b91af">MarshalAs</span>(System.Runtime.InteropServices.<span style="color: #2b91af">UnmanagedType</span>.ByValArray, SizeConst = 256)]
            <span style="color: blue">public uint</span>[] cols;
        }

        <span style="color: blue">static uint </span>MAKERGB(<span style="color: blue">int </span>r, <span style="color: blue">int </span>g, <span style="color: blue">int </span>b)
        {
            <span style="color: blue">return </span>((<span style="color: blue">uint</span>)(b &amp; 255)) | ((<span style="color: blue">uint</span>)((r &amp; 255) &lt;&lt; 8)) | ((<span style="color: blue">uint</span>)((g &amp; 255) &lt;&lt; 16));
        }
        <span style="color: blue">#endregion

        </span><span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Converts the given bitmap to a monochrome tiff bitmap.
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;sourceBitmap&quot;&gt;</span><span style="color: green">The source bitmap.</span><span style="color: gray">&lt;/param&gt;
        /// &lt;returns&gt;&lt;/returns&gt;
        </span><span style="color: blue">public static </span><span style="color: #2b91af">Bitmap </span>ConvertToMonochromeTiff(<span style="color: blue">this </span><span style="color: #2b91af">Bitmap </span>sourceBitmap)
        {
            <span style="color: #2b91af">Bitmap </span>destination = <span style="color: blue">null</span>;
            <span style="color: blue">int </span>bpp = 1;                                                            <span style="color: green">// Amount of bits to use in pallet, for monochrome use 1 bit (0 = black, 1 = white).
            </span><span style="color: blue">uint </span>ncols = (<span style="color: blue">uint</span>)1 &lt;&lt; bpp;                                            <span style="color: green">// Use 2 colours (black and white) for monochrome tiff.
            </span><span style="color: blue">int </span>width = sourceBitmap.Width;
            <span style="color: blue">int </span>height = sourceBitmap.Height;
            <span style="color: blue">uint </span>size = (<span style="color: blue">uint</span>)(((width + 7) &amp; 0xFFFFFFF8) * height / 8);
            <span style="color: blue">uint</span>[] pallet = <span style="color: blue">new uint</span>[256];                                          <span style="color: green">// Pallet has a fixed size 256, even when we are using fewer colours.
            </span>pallet[0] = MAKERGB(0, 0, 0);                                           <span style="color: green">// Create black pixel.
            </span>pallet[1] = MAKERGB(255, 255, 255);                                     <span style="color: green">// Create white pixel.
            </span>BITMAPINFO bmi = <span style="color: blue">new </span>BITMAPINFO()                                       <span style="color: green">// Create unmanaged monochrome bitmapinfo.
            </span>{
                biSize = 40,                                                        <span style="color: green">// The size of the BITMAPHEADERINFO struct.
                </span>biWidth = width,
                biHeight = height,
                biPlanes = 1,
                biBitCount = (<span style="color: blue">short</span>)bpp,                                            <span style="color: green">// Amount of bits per pixel (1 for monochrome).
                </span>biCompression = BI_RGB,
                biSizeImage = size,
                biXPelsPerMeter = 1000000,
                biYPelsPerMeter = 1000000,
                biClrUsed = ncols,
                biClrImportant = ncols,
                cols = pallet
            };

            IntPtr sourceHbitmap = sourceBitmap.GetHbitmap();                       <span style="color: green">// Convert bitmap to unmanaged HBitmap.
            </span>IntPtr bits0;                                                           <span style="color: green">// Pointer to the raw bits that make up the bitmap.
            </span>IntPtr destinationHbitmap = CreateDIBSection
            (
                IntPtr.Zero,
                <span style="color: blue">ref </span>bmi,
                DIB_RGB_COLORS,
                <span style="color: blue">out </span>bits0,
                IntPtr.Zero,
                0
            );                                                                      <span style="color: green">// Create the indexed bitmap.
            </span>IntPtr screenDC = GetDC(IntPtr.Zero);                                   <span style="color: green">// Obtain the DC (= GDI equivalent of &quot;Graphics&quot; in GDI+) for the screen.
            </span>IntPtr sourceDC = CreateCompatibleDC(screenDC);                         <span style="color: green">// Create a DC for the original hbitmap.
            </span>SelectObject(sourceDC, sourceHbitmap);
            IntPtr destinationDC = CreateCompatibleDC(screenDC);                    <span style="color: green">// Create a DC for the monochrome hbitmap.
            </span>SelectObject(destinationDC, destinationHbitmap);
            BitBlt(destinationDC, 0, 0, width, height, sourceDC, 0, 0, SRCCOPY);    <span style="color: green">// Use GDI's BitBlt function to copy from original hbitmap into monocrhome bitmap.
            </span>destination = System.Drawing.<span style="color: #2b91af">Bitmap</span>.FromHbitmap(destinationHbitmap);    <span style="color: green">// Convert this monochrome hbitmap back into a Bitmap.

            // Cleanup.
            </span>DeleteDC(sourceDC);
            DeleteDC(destinationDC);
            ReleaseDC(IntPtr.Zero, screenDC);
            DeleteObject(sourceHbitmap);
            DeleteObject(destinationHbitmap);

            <span style="color: blue">return </span>destination;
        }
    }
}</pre>
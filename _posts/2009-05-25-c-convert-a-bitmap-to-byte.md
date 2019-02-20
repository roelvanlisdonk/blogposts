---
ID: 475
post_title: 'C# convert a BitMap to Byte[]'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/25/c-convert-a-bitmap-to-byte/
published: true
post_date: 2009-05-25 12:57:30
---
<div class="padten">   <div class="ms-inputuserfield padfive seventyp">     <div>       <div class="ExternalClass427972A24B7F4B9399E1EDF659992FA1">         <pre class="code"><span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Covert a bitmap to a byte array
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;bitmap&quot;&gt;&lt;/param&gt;
        /// &lt;returns&gt;
        /// </span><span style="color: green">byte array, when bitmap could be converted
        </span><span style="color: gray">/// </span><span style="color: green">null, when bitmap is null
        </span><span style="color: gray">/// </span><span style="color: green">null, when bitmap could not be converted to byte array
        </span><span style="color: gray">/// &lt;/returns&gt;
        </span><span style="color: blue">public byte</span>[] ConvertBitMapToByteArray(<span style="color: #2b91af">Bitmap </span>bitmap)
        {
            <span style="color: blue">byte</span>[] result = <span style="color: blue">null</span>;

            <span style="color: blue">if </span>(bitmap != <span style="color: blue">null</span>)
            {
                <span style="color: #2b91af">MemoryStream </span>stream = <span style="color: blue">new </span><span style="color: #2b91af">MemoryStream</span>();
                bitmap.Save(stream, bitmap.RawFormat);
                result = stream.ToArray();
            }

            <span style="color: blue">return </span>result;
        }</pre>
      </div>
    </div>
  </div>
</div>
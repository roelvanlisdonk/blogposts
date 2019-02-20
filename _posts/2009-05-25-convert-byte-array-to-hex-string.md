---
ID: 477
post_title: 'Convert byte [] array to hex string'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/25/convert-byte-array-to-hex-string/
published: true
post_date: 2009-05-25 13:13:27
---
<div class="padten">   <div class="ms-inputuserfield padfive seventyp">     <div>       <div class="ExternalClassB14AF5491E6141118DB75AC4D5081833">         <pre class="code"><span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Convert a byte array to a hex string
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;bytes&quot;&gt;&lt;/param&gt;
        /// &lt;returns&gt;
        ///     </span><span style="color: green">Converted byte array to string
        </span><span style="color: gray">///     </span><span style="color: green">null, when bytes == null
        </span><span style="color: gray">/// &lt;/returns&gt;
        </span><span style="color: blue">public string </span>ConvertByteArrayToString(<span style="color: blue">byte</span>[] bytes)
        {
            <span style="color: blue">string </span>result = <span style="color: blue">null</span>;

            <span style="color: green">// Convert byte array to string, when bytes is not null
            </span><span style="color: blue">if </span>(bytes != <span style="color: blue">null</span>)
            {
                result = <span style="color: #2b91af">BitConverter</span>.ToString(bytes);
                result = result.Replace(<span style="color: #a31515">&quot;-&quot;</span>, <span style="color: blue">string</span>.Empty);
            }

            <span style="color: blue">return </span>result;
        }</pre>
      </div>
    </div>
  </div>
</div>
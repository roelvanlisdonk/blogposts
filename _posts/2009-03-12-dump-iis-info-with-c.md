---
ID: 283
post_title: 'Dump IIS info with C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/03/12/dump-iis-info-with-c/
published: true
post_date: 2009-03-12 15:31:14
---
<pre class="code"><span style="color:gray;"><span style="color: #000000;"><span style="color: #008000; font-size: x-small;"><span style="color: #008000; font-size: x-small;"><span style="color: #a31515; font-size: x-small;"><span style="color: #a31515; font-size: x-small;">To call the function use:  this.DumpIISInfo(new DirectoryEntry("IIS://localhost/w3svc"));</span></span></span></span></span></span></pre>
<pre class="code"><span style="color:gray;">/// &lt;summary&gt;
        /// </span><span style="color:green;">Dump iis info
        </span><span style="color:gray;">/// &lt;/summary&gt;
        /// &lt;returns&gt;
        /// </span><span style="color:green;">0 = All IIS information is written to the console
        </span><span style="color:gray;">/// </span><span style="color:green;">1 = Parameter entry was null
        </span><span style="color:gray;">/// &lt;/returns&gt;
        </span><span style="color:blue;">public int </span>DumpIISInfo(<span style="color:#2b91af;">DirectoryEntry </span>entry)
        {
            <span style="color:blue;">if </span>(entry == <span style="color:blue;">null</span>) { <span style="color:blue;">return </span>1; }

            <span style="color:blue;">foreach </span>(<span style="color:#2b91af;">DirectoryEntry </span>childEntry <span style="color:blue;">in </span>entry.Children)
            {
                <span style="color:blue;">using </span>(childEntry)
                {
                    <span style="color:#2b91af;">Console</span>.WriteLine(<span style="color:blue;">string</span>.Format(<span style="color:#a31515;">"Child name [{0}]"</span>, childEntry.Name));
                    <span style="color:blue;">foreach </span>(<span style="color:#2b91af;">PropertyValueCollection </span>property <span style="color:blue;">in </span>childEntry.Properties)
                    {
                        <span style="color:#2b91af;">Console</span>.WriteLine(<span style="color:blue;">string</span>.Format(<span style="color:#a31515;">"[{0}] [{1}] [{2}]"</span>, childEntry.Name, property.PropertyName, property.Value));
                    }
                    <span style="color:blue;">if </span>(childEntry.Children != <span style="color:blue;">null</span>)
                    {
                        <span style="color:blue;">this</span>.DumpIISInfo(childEntry);
                    }
                }
            }

            <span style="color:blue;">return </span>0;
        }</pre>
<a href="http://11011.net/software/vspaste"></a>

<a href="http://11011.net/software/vspaste"></a>
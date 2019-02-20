---
ID: 282
post_title: 'Determine if an IIS website or IIS virtualdirectory exist, that run under a given applicationpool, with C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/03/12/determine-if-an-iis-website-or-iis-virtualdirectory-exist-that-run-under-a-given-applicationpool-with-c/
published: true
post_date: 2009-03-12 09:13:31
---
<pre class="code"><span style="color:gray;">To call this function use: DoesAppPoolHaveWebsites(new DirectoryEntry(string.Format("IIS://{0}/w3svc", "localhost")), "appPoolName")</span></pre><pre class="code"><span style="color:gray;"></span>&nbsp;</pre><pre class="code"><span style="color:gray;">        /// &lt;summary&gt;
        /// </span><span style="color:green;">Determine if a IIS website running under an applicationpool exists.
        </span><span style="color:gray;">/// &lt;/summary&gt;
        /// &lt;returns&gt;&lt;/returns&gt;
        </span><span style="color:blue;">public bool </span>DoesAppPoolHaveWebsites(<span style="color:#2b91af;">DirectoryEntry </span>iisEntry, <span style="color:blue;">string </span>appPoolName)
        {
            <span style="color:blue;">bool </span>result = <span style="color:blue;">false</span>;
            <span style="color:blue;">if </span>(iisEntry == <span style="color:blue;">null</span>) { <span style="color:blue;">throw new </span><span style="color:#2b91af;">Exception</span>(<span style="color:#a31515;">"Parameter [iisEntry] can't be null or empty"</span>); }
            <span style="color:blue;">if </span>(<span style="color:blue;">string</span>.IsNullOrEmpty(appPoolName)) { <span style="color:blue;">throw new </span><span style="color:#2b91af;">Exception</span>(<span style="color:#a31515;">"Parameter [appPoolName] can't be null or empty"</span>); }


            <span style="color:blue;">foreach </span>(<span style="color:#2b91af;">DirectoryEntry </span>child <span style="color:blue;">in </span>iisEntry.Children)
            {
                <span style="color:blue;">foreach </span>(<span style="color:#2b91af;">PropertyValueCollection </span>property <span style="color:blue;">in </span>child.Properties)
                {
                    <span style="color:blue;">if </span>(property.PropertyName.Equals(<span style="color:#a31515;">"AppPoolId"</span>, <span style="color:#2b91af;">StringComparison</span>.OrdinalIgnoreCase))
                    {
                        <span style="color:blue;">if </span>(property.Value != <span style="color:blue;">null</span>)
                        {
                            <span style="color:blue;">if </span>(property.Value.ToString().Equals(appPoolName, <span style="color:#2b91af;">StringComparison</span>.OrdinalIgnoreCase))
                            {
                                result = <span style="color:blue;">true</span>;
                                <span style="color:blue;">break</span>;
                            }
                        }
                    }
                }
                <span style="color:blue;">if </span>(result)
                {
                    <span style="color:blue;">break</span>;
                }
                <span style="color:blue;">else
                </span>{
                    <span style="color:blue;">if </span>(child.Children != <span style="color:blue;">null</span>)
                    {
                        <span style="color:blue;">if </span>(<span style="color:blue;">this</span>.DoesAppPoolHaveWebsites(child, appPoolName))
                        {
                            result = <span style="color:blue;">true</span>;
                        }
                    }
                }
            }

            <span style="color:blue;">return </span>result;
        }
</pre><a href="http://11011.net/software/vspaste"></a>
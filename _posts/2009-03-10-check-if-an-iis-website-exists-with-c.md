---
ID: 270
post_title: 'Check if an IIS website exists with C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/03/10/check-if-an-iis-website-exists-with-c/
published: true
post_date: 2009-03-10 10:20:45
---
<p></p><pre class="code"><span style="color:gray;">        /// &lt;summary&gt;
        /// </span><span style="color:green;">Check if a website on the given server exist.
        </span><span style="color:gray;">/// </span><span style="color:green;">Check on websitename (ServerComment) is case insensitive.
        </span><span style="color:gray;">/// &lt;/summary&gt;
        /// &lt;param name="serverName"&gt;</span><span style="color:green;">Name of the IIS server e.g. localhost</span><span style="color:gray;">&lt;/param&gt;
        /// &lt;param name="websiteName"&gt;</span><span style="color:green;">Name of the website e.g. test</span><span style="color:gray;">&lt;/param&gt;
        /// &lt;returns&gt;&lt;/returns&gt;
        </span><span style="color:blue;">public bool </span>DoesWebsiteExist(<span style="color:blue;">string </span>serverName, <span style="color:blue;">string </span>websiteName)
        {
            <span style="color:blue;">bool </span>result = <span style="color:blue;">false</span>;

            <span style="color:#2b91af;">DirectoryEntry </span>w3svc = <span style="color:blue;">new </span><span style="color:#2b91af;">DirectoryEntry</span>(<span style="color:blue;">string</span>.Format(<span style="color:#a31515;">"IIS://{0}/w3svc"</span>, serverName));

            <span style="color:blue;">foreach </span>(<span style="color:#2b91af;">DirectoryEntry </span>site <span style="color:blue;">in </span>w3svc.Children)
            {
                <span style="color:blue;">if </span>(site.Properties[<span style="color:#a31515;">"ServerComment"</span>] != <span style="color:blue;">null</span>)
                {
                    <span style="color:blue;">if </span>(site.Properties[<span style="color:#a31515;">"ServerComment"</span>].Value != <span style="color:blue;">null</span>)
                    {
                        <span style="color:blue;">if </span>(<span style="color:blue;">string</span>.Compare(site.Properties[<span style="color:#a31515;">"ServerComment"</span>].Value.ToString(), websiteName, <span style="color:blue;">false</span>) == 0)
                        {
                            result = <span style="color:blue;">true</span>;
                        }
                    }
                }
            }

            <span style="color:blue;">return </span>result;
        }</pre><a href="http://11011.net/software/vspaste"></a>
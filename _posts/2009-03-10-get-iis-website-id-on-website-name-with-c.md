---
ID: 271
post_title: 'Get IIS website id on website name, with C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/03/10/get-iis-website-id-on-website-name-with-c/
published: true
post_date: 2009-03-10 10:47:17
---
<pre class="code"><span style="color:gray;">        /// &lt;summary&gt;
        /// </span><span style="color:green;">Get website id on websitename
        </span><span style="color:gray;">/// &lt;/summary&gt;
        /// &lt;param name="serverName"&gt;</span><span style="color:green;">Name of the IIS server e.g. localhost</span><span style="color:gray;">&lt;/param&gt;
        /// &lt;param name="websiteName"&gt;</span><span style="color:green;">Name of the website e.g. test</span><span style="color:gray;">&lt;/param&gt;
        /// &lt;returns&gt;
        /// </span><span style="color:green;">Less the 0, site does not exist
        </span><span style="color:gray;">/// </span><span style="color:green;">Id of the existing site
        </span><span style="color:gray;">/// &lt;/returns&gt;
        </span><span style="color:blue;">public int </span>GetWebSiteId(<span style="color:blue;">string </span>serverName, <span style="color:blue;">string </span>websiteName)
        {
            <span style="color:blue;">int </span>result = -1;

            <span style="color:#2b91af;">DirectoryEntry </span>w3svc = <span style="color:blue;">new </span><span style="color:#2b91af;">DirectoryEntry</span>(<span style="color:blue;">string</span>.Format(<span style="color:#a31515;">"IIS://{0}/w3svc"</span>, serverName));

            <span style="color:blue;">foreach </span>(<span style="color:#2b91af;">DirectoryEntry </span>site <span style="color:blue;">in </span>w3svc.Children)
            {
                <span style="color:blue;">if </span>(site.Properties[<span style="color:#a31515;">"ServerComment"</span>] != <span style="color:blue;">null</span>)
                {
                    <span style="color:blue;">if </span>(site.Properties[<span style="color:#a31515;">"ServerComment"</span>].Value != <span style="color:blue;">null</span>)
                    {
                        <span style="color:blue;">if </span>(<span style="color:blue;">string</span>.Compare(site.Properties[<span style="color:#a31515;">"ServerComment"</span>].Value.ToString(), websiteName, </pre><pre class="code"><span style="color:blue;">                         false</span>) == 0)
                        {
                            result = site.Name;
                            <span style="color:blue;">break</span>;
                        }
                    }
                }
            }

            <span style="color:blue;">return </span>result;
        }</pre><a href="http://11011.net/software/vspaste"></a>
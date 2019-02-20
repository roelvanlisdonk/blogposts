---
ID: 272
post_title: 'Get or set the filesystem folder (path) for a IIS website, with C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/03/10/get-the-filesystem-folder-path-for-a-iis-website-with-c/
published: true
post_date: 2009-03-10 13:03:18
---
<pre class="code"><span style="color:gray;">        /// &lt;summary&gt;
        /// </span><span style="color:green;">Get the filesystem folder for the given website
        </span><span style="color:gray;">/// &lt;/summary&gt;
        /// &lt;param name="serverName"&gt;</span><span style="color:green;">Name of the IIS server e.g. localhost</span><span style="color:gray;">&lt;/param&gt;
        /// &lt;param name="websiteName"&gt;</span><span style="color:green;">Name of the website e.g. test</span><span style="color:gray;">&lt;/param&gt;
        /// &lt;returns&gt;</span><span style="color:green;">filesystem folder or empty if not found</span><span style="color:gray;">&lt;/returns&gt;
        </span><span style="color:blue;">public string </span>GetWebSiteFileSystemFolder(<span style="color:blue;">string </span>serverName, <span style="color:blue;">string </span>websiteName)
        {
            <span style="color:blue;">if </span>(<span style="color:blue;">string</span>.IsNullOrEmpty(serverName)) { <span style="color:blue;">throw new </span><span style="color:#2b91af;">Exception</span>(<span style="color:#a31515;">"Parameter [serverName] can't be null or empty"</span>); }
            <span style="color:blue;">if </span>(<span style="color:blue;">string</span>.IsNullOrEmpty(websiteName)) { <span style="color:blue;">throw new </span><span style="color:#2b91af;">Exception</span>(<span style="color:#a31515;">"Parameter [websiteName] can't be null or empty"</span>); }
            <span style="color:blue;">string </span>result = <span style="color:blue;">string</span>.Empty;

            <span style="color:#2b91af;">DirectoryEntry </span>w3svc = <span style="color:blue;">new </span><span style="color:#2b91af;">DirectoryEntry</span>(<span style="color:blue;">string</span>.Format(<span style="color:#a31515;">"IIS://{0}/w3svc"</span>, serverName));

            <span style="color:blue;">foreach </span>(<span style="color:#2b91af;">DirectoryEntry </span>site <span style="color:blue;">in </span>w3svc.Children)
            {
                <span style="color:blue;">if </span>(site.Properties[<span style="color:#a31515;">"ServerComment"</span>] != <span style="color:blue;">null</span>)
                {
                    <span style="color:blue;">if </span>(site.Properties[<span style="color:#a31515;">"ServerComment"</span>].Value != <span style="color:blue;">null</span>)
                    {
                        <span style="color:blue;">if </span>(<span style="color:blue;">string</span>.Compare(site.Properties[<span style="color:#a31515;">"ServerComment"</span>].Value.ToString(), websiteName, <span style="color:blue;">false</span>) == 0)
                        {

                            <span style="color:blue;">foreach </span>(<span style="color:#2b91af;">DirectoryEntry </span>child <span style="color:blue;">in </span>site.Children)
                            {
                                <span style="color:blue;">if </span>(child.Properties[<span style="color:#a31515;">"Path"</span>] != <span style="color:blue;">null</span>)
                                {
                                    <span style="color:blue;">if </span>(child.Properties[<span style="color:#a31515;">"Path"</span>].Value != <span style="color:blue;">null</span>)
                                    {
                                        result = child.Properties[<span style="color:#a31515;">"Path"</span>].Value.ToString();
                                        <span style="color:blue;">break</span>;
                                    }
                                }
                            }
                        }
                    }
                }
            }

            <span style="color:blue;">return </span>result;
        }</pre><pre class="code">&nbsp;</pre>
<h4>Change the Propery "Path" to "ServerBindings" to change serverbindings like ":80:testwebsite"</h4><a href="http://11011.net/software/vspaste"></a>
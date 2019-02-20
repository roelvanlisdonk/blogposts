---
ID: 286
post_title: 'Delete IIS6 or IIS7 virtual directory on a website with hostheader, with C# and NANT'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/03/16/delete-iis6-or-iis7-virtual-directory-on-a-website-with-hostheader-with-c-and-nant/
published: true
post_date: 2009-03-16 15:05:56
---
<pre class="code"><span style="color:blue;">using </span>System;
<span style="color:blue;">using </span>System.DirectoryServices;
<span style="color:blue;">using </span>System.Globalization;
<span style="color:blue;">using </span>Ada.Configurator.Common;
<span style="color:blue;">using </span>NAnt.Core.Attributes;
<span style="color:blue;">using </span>NAnt.Core;

<span style="color:blue;">namespace </span>AdaNantTasks
{
    <span style="color:gray;">/// &lt;summary&gt;
    /// </span><span style="color:green;">Delete an IIS virtual directory on a website with a hostheader.
    </span><span style="color:gray;">/// &lt;/summary&gt;
    </span>[<span style="color:#2b91af;">TaskName</span>(<span style="color:#a31515;">"deleteVirtualDirectoryTask"</span>)]
    <span style="color:blue;">public class </span><span style="color:#2b91af;">DeleteVirtualDirectoryTask </span>: <span style="color:#2b91af;">Task
    </span>{
        <span style="color:blue;">public </span><span style="color:#2b91af;">NantLogger </span>logger = <span style="color:blue;">new </span><span style="color:#2b91af;">NantLogger</span>();
        <span style="color:blue;">public string </span>VirDirSchemaName = <span style="color:#a31515;">"IIsWebVirtualDir"</span>;

        <span style="color:blue;">private string </span>m_server;
        [<span style="color:#2b91af;">TaskAttribute</span>(<span style="color:#a31515;">"server"</span>, Required = <span style="color:blue;">true</span>)]
        [<span style="color:#2b91af;">StringValidator</span>(AllowEmpty = <span style="color:blue;">false</span>)]
        <span style="color:blue;">public string </span>Server
        {
            <span style="color:blue;">get </span>{ <span style="color:blue;">return </span>m_server; }
            <span style="color:blue;">set </span>{ m_server = <span style="color:blue;">value</span>; }
        }

        <span style="color:blue;">private string </span>m_virtualDirectoryName;
        [<span style="color:#2b91af;">TaskAttribute</span>(<span style="color:#a31515;">"virtualDirectoryName"</span>, Required = <span style="color:blue;">true</span>)]
        [<span style="color:#2b91af;">StringValidator</span>(AllowEmpty = <span style="color:blue;">false</span>)]
        <span style="color:blue;">public string </span>VirtualDirectoryName
        {
            <span style="color:blue;">get </span>{ <span style="color:blue;">return </span>m_virtualDirectoryName; }
            <span style="color:blue;">set </span>{ m_virtualDirectoryName = <span style="color:blue;">value</span>; }
        }

        <span style="color:blue;">private string </span>m_websiteName;
        [<span style="color:#2b91af;">TaskAttribute</span>(<span style="color:#a31515;">"websiteName"</span>, Required = <span style="color:blue;">true</span>)]
        [<span style="color:#2b91af;">StringValidator</span>(AllowEmpty = <span style="color:blue;">false</span>)]
        <span style="color:blue;">public string </span>WebsiteName
        {
            <span style="color:blue;">get </span>{ <span style="color:blue;">return </span>m_websiteName; }
            <span style="color:blue;">set </span>{ m_websiteName = <span style="color:blue;">value</span>; }
        }

        <span style="color:gray;">/// &lt;summary&gt;
        /// </span><span style="color:green;">Creates website
        </span><span style="color:gray;">/// &lt;/summary&gt;
        </span><span style="color:blue;">protected override void </span>ExecuteTask()
        {
            <span style="color:blue;">try
            </span>{
                <span style="color:blue;">this</span>.DeleteVirtualDirectory();
                Project.Log(<span style="color:#2b91af;">Level</span>.Info, <span style="color:blue;">string</span>.Format(<span style="color:#a31515;">"Virtualdirectory [{0}] created"</span>, m_virtualDirectoryName));
            }
            <span style="color:blue;">catch </span>(<span style="color:#2b91af;">Exception </span>ex)
            {
                logger.Log(<span style="color:blue;">this</span>.Project, <span style="color:#2b91af;">Level</span>.Error, <span style="color:blue;">string</span>.Format(<span style="color:#a31515;">"VirtualDirectory [{0}] not created, because an exception occurred [{1}]"</span>, m_virtualDirectoryName, ex.ToString()));
                <span style="color:blue;">throw new </span><span style="color:#2b91af;">BuildException</span>(<span style="color:#a31515;">"Unable to create website"</span>, ex);
            }
        }

        <span style="color:gray;">/// &lt;summary&gt;
        /// </span><span style="color:green;">Delete an IIS virtualdirectory
        </span><span style="color:gray;">/// &lt;/summary&gt;
        </span><span style="color:blue;">public void </span>DeleteVirtualDirectory()
        {
            <span style="color:blue;">if </span>(<span style="color:blue;">string</span>.IsNullOrEmpty(m_server)) { <span style="color:blue;">throw new </span><span style="color:#2b91af;">Exception</span>(<span style="color:#a31515;">"Property [Server] can't be null or empty"</span>); } <span style="color:blue;">else </span>{ <span style="color:#2b91af;">Console</span>.WriteLine(<span style="color:blue;">string</span>.Format(<span style="color:#a31515;">"DeleteVirtualDirectory: [{0}]"</span>, m_server)); }
            <span style="color:blue;">if </span>(<span style="color:blue;">string</span>.IsNullOrEmpty(m_virtualDirectoryName)) { <span style="color:blue;">throw new </span><span style="color:#2b91af;">Exception</span>(<span style="color:#a31515;">"Property [VirtualDirectoryName] can't be null or empty"</span>); } <span style="color:blue;">else </span>{ <span style="color:#2b91af;">Console</span>.WriteLine(<span style="color:blue;">string</span>.Format(<span style="color:#a31515;">"DeleteVirtualDirectory: [{0}]"</span>, m_virtualDirectoryName)); }
            <span style="color:blue;">if </span>(<span style="color:blue;">string</span>.IsNullOrEmpty(m_websiteName)) { <span style="color:blue;">throw new </span><span style="color:#2b91af;">Exception</span>(<span style="color:#a31515;">"Property [WebsiteName] can't be null or empty"</span>); } <span style="color:blue;">else </span>{ <span style="color:#2b91af;">Console</span>.WriteLine(<span style="color:blue;">string</span>.Format(<span style="color:#a31515;">"DeleteVirtualDirectory: [{0}]"</span>, m_websiteName)); }

            <span style="color:blue;">int </span>websiteId = <span style="color:blue;">this</span>.GetWebSiteId(m_server, m_websiteName);

            <span style="color:blue;">string </span>iisPath = <span style="color:blue;">string</span>.Format(<span style="color:#a31515;">"IIS://{0}/w3svc/{1}"</span>, m_server, websiteId);

            <span style="color:blue;">using </span>(<span style="color:#2b91af;">DirectoryEntry </span>w3svc = <span style="color:blue;">new </span><span style="color:#2b91af;">DirectoryEntry</span>(iisPath))
            {
                w3svc.RefreshCache();

                <span style="color:blue;">using </span>(<span style="color:#2b91af;">DirectoryEntry </span>folderRoot = w3svc.Children.Find(<span style="color:#a31515;">"Root"</span>, VirDirSchemaName))
                {
                    folderRoot.RefreshCache();
                    <span style="color:#2b91af;">DirectoryEntry </span>virtualDirectory = <span style="color:blue;">null</span>;

                    <span style="color:blue;">try
                    </span>{
                        folderRoot.Children.Find(m_virtualDirectoryName, VirDirSchemaName);
                        folderRoot.Invoke(<span style="color:#a31515;">"AppDelete"</span>);
                        folderRoot.Children.Remove(virtualDirectory);
                    }
                    <span style="color:blue;">catch
                    </span>{
                        <span style="color:#2b91af;">Console</span>.WriteLine(<span style="color:#a31515;">"Virtual directory [{0}] already exists or error during delete"</span>, m_virtualDirectoryName);
                    }
                }
            }
        }

        <span style="color:gray;">/// &lt;summary&gt;
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
            <span style="color:blue;">if </span>(<span style="color:blue;">string</span>.IsNullOrEmpty(serverName)) { <span style="color:blue;">throw new </span><span style="color:#2b91af;">Exception</span>(<span style="color:#a31515;">"Parameter [serverName] can't be null or empty"</span>); } <span style="color:blue;">else </span>{ <span style="color:#2b91af;">Console</span>.WriteLine(<span style="color:blue;">string</span>.Format(<span style="color:#a31515;">"GetWebSiteId: [{0}]"</span>, serverName)); }
            <span style="color:blue;">if </span>(<span style="color:blue;">string</span>.IsNullOrEmpty(websiteName)) { <span style="color:blue;">throw new </span><span style="color:#2b91af;">Exception</span>(<span style="color:#a31515;">"Parameter [websiteName] can't be null or empty"</span>); } <span style="color:blue;">else </span>{ <span style="color:#2b91af;">Console</span>.WriteLine(<span style="color:blue;">string</span>.Format(<span style="color:#a31515;">"GetWebSiteId: [{0}]"</span>, websiteName)); }
            <span style="color:blue;">int </span>result = -1;

            <span style="color:blue;">using </span>(<span style="color:#2b91af;">DirectoryEntry </span>w3svc = <span style="color:blue;">new </span><span style="color:#2b91af;">DirectoryEntry</span>(<span style="color:blue;">string</span>.Format(<span style="color:#a31515;">"IIS://{0}/w3svc"</span>, serverName)))
            {
                w3svc.RefreshCache();

                <span style="color:blue;">foreach </span>(<span style="color:#2b91af;">DirectoryEntry </span>site <span style="color:blue;">in </span>w3svc.Children)
                {
                    <span style="color:blue;">using </span>(site)
                    {
                        site.RefreshCache();

                        <span style="color:blue;">if </span>(site.Properties[<span style="color:#a31515;">"ServerComment"</span>] != <span style="color:blue;">null</span>)
                        {
                            <span style="color:blue;">if </span>(site.Properties[<span style="color:#a31515;">"ServerComment"</span>].Value != <span style="color:blue;">null</span>)
                            {
                                <span style="color:blue;">if </span>(site.Properties[<span style="color:#a31515;">"ServerComment"</span>].Value.ToString().Equals(websiteName, <span style="color:#2b91af;">StringComparison</span>.OrdinalIgnoreCase))
                                {
                                    result = <span style="color:blue;">int</span>.Parse(site.Name);
                                }
                            }
                        }
                    }
                }
            }

            <span style="color:#2b91af;">Console</span>.WriteLine(<span style="color:blue;">string</span>.Format(<span style="color:#a31515;">"GetWebSiteId: [{0}]"</span>, result));
            <span style="color:blue;">return </span>result;
        }
    }
}
</pre><a href="http://11011.net/software/vspaste"></a><a href="http://11011.net/software/vspaste"></a>
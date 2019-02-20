---
ID: 285
post_title: 'Create IIS6 or IIS7 virtual directory on a website with hostheader, with C# and NANT'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/03/16/create-iis6-or-iis7-virtual-directory-on-a-website-with-hostheader-with-c-and-nant/
published: true
post_date: 2009-03-16 15:01:58
---
<pre class="code"><span style="color:blue;">using </span>System;
<span style="color:blue;">using </span>System.DirectoryServices;
<span style="color:blue;">using </span>System.Globalization;
<span style="color:blue;">using </span>Ada.Configurator.Common;
<span style="color:blue;">using </span>NAnt.Core.Attributes;
<span style="color:blue;">using </span>NAnt.Core;

<span style="color:blue;">namespace </span>AdaNantTasks
{
    [<span style="color:#2b91af;">TaskName</span>(<span style="color:#a31515;">"createWebSite"</span>)]
    <span style="color:blue;">public class </span><span style="color:#2b91af;">CreateWebsiteTask </span>: <span style="color:#2b91af;">Task
    </span>{
        <span style="color:blue;">public </span><span style="color:#2b91af;">NantLogger </span>logger = <span style="color:blue;">new </span><span style="color:#2b91af;">NantLogger</span>();

        <span style="color:blue;">private string </span>m_server;
        [<span style="color:#2b91af;">TaskAttribute</span>(<span style="color:#a31515;">"server"</span>, Required = <span style="color:blue;">true</span>)]
        [<span style="color:#2b91af;">StringValidator</span>(AllowEmpty = <span style="color:blue;">false</span>)]
        <span style="color:blue;">public string </span>Server
        {
            <span style="color:blue;">get </span>{ <span style="color:blue;">return </span>m_server; }
            <span style="color:blue;">set </span>{ m_server = <span style="color:blue;">value</span>; }
        }

        <span style="color:blue;">private string </span>m_websiteName;
        [<span style="color:#2b91af;">TaskAttribute</span>(<span style="color:#a31515;">"websiteName"</span>, Required = <span style="color:blue;">true</span>)]
        [<span style="color:#2b91af;">StringValidator</span>(AllowEmpty = <span style="color:blue;">false</span>)]
        <span style="color:blue;">public string </span>WebsiteName
        {
            <span style="color:blue;">get </span>{ <span style="color:blue;">return </span>m_websiteName; }
            <span style="color:blue;">set </span>{ m_websiteName = <span style="color:blue;">value</span>; }
        }

        <span style="color:blue;">private string </span>m_binding;
        [<span style="color:#2b91af;">TaskAttribute</span>(<span style="color:#a31515;">"binding"</span>, Required = <span style="color:blue;">true</span>)]
        [<span style="color:#2b91af;">StringValidator</span>(AllowEmpty = <span style="color:blue;">false</span>)]
        <span style="color:blue;">public string </span>Binding
        {
            <span style="color:blue;">get </span>{ <span style="color:blue;">return </span>m_binding; }
            <span style="color:blue;">set </span>{ m_binding = <span style="color:blue;">value</span>; }
        }

        <span style="color:blue;">private string </span>m_webFolder;
        [<span style="color:#2b91af;">TaskAttribute</span>(<span style="color:#a31515;">"webFolder"</span>, Required = <span style="color:blue;">true</span>)]
        [<span style="color:#2b91af;">StringValidator</span>(AllowEmpty = <span style="color:blue;">false</span>)]
        <span style="color:blue;">public string </span>WebFolder
        {
            <span style="color:blue;">get </span>{ <span style="color:blue;">return </span>m_webFolder; }
            <span style="color:blue;">set </span>{ m_webFolder = <span style="color:blue;">value</span>; }
        }

        <span style="color:blue;">private string </span>m_appPool;
        [<span style="color:#2b91af;">TaskAttribute</span>(<span style="color:#a31515;">"appPool"</span>, Required = <span style="color:blue;">true</span>)]
        [<span style="color:#2b91af;">StringValidator</span>(AllowEmpty = <span style="color:blue;">false</span>)]
        <span style="color:blue;">public string </span>AppPool
        {
            <span style="color:blue;">get </span>{ <span style="color:blue;">return </span>m_appPool; }
            <span style="color:blue;">set </span>{ m_appPool = <span style="color:blue;">value</span>; }
        }

        <span style="color:gray;">/// &lt;summary&gt;
        /// </span><span style="color:green;">Creates website
        </span><span style="color:gray;">/// &lt;/summary&gt;
        </span><span style="color:blue;">protected override void </span>ExecuteTask()
        {
            <span style="color:blue;">try
            </span>{
                <span style="color:blue;">int </span>result = CreateWebsite();
                <span style="color:blue;">switch </span>(result)
                {
                    <span style="color:blue;">case </span>0:
                        Project.Log(<span style="color:#2b91af;">Level</span>.Info, <span style="color:blue;">string</span>.Format(<span style="color:#a31515;">"Website [{0}] not created, because it already exists"</span>, m_websiteName));
                        <span style="color:blue;">break</span>;
                    <span style="color:blue;">default</span>:
                        Project.Log(<span style="color:#2b91af;">Level</span>.Info, <span style="color:blue;">string</span>.Format(<span style="color:#a31515;">"Website [{0}] created"</span>, m_websiteName));
                        <span style="color:blue;">break</span>;
                }
            }
            <span style="color:blue;">catch </span>(<span style="color:#2b91af;">Exception </span>ex)
            {
                logger.Log(<span style="color:blue;">this</span>.Project, <span style="color:#2b91af;">Level</span>.Error, <span style="color:blue;">string</span>.Format(<span style="color:#a31515;">"Website [{0}] not created, because an exception occurred [{1}]"</span>, m_websiteName, ex.ToString()));
                <span style="color:blue;">throw new </span><span style="color:#2b91af;">BuildException</span>(<span style="color:#a31515;">"Unable to create website"</span>, ex);
            }
        }

        <span style="color:gray;">/// &lt;summary&gt;
        /// </span><span style="color:green;">Create an IIS website.
        </span><span style="color:gray;">/// &lt;/summary&gt;
        /// &lt;returns&gt;</span><span style="color:green;">Website id</span><span style="color:gray;">&lt;/returns&gt;
        </span><span style="color:blue;">public int </span>CreateWebsite()
        {
            <span style="color:blue;">if </span>(<span style="color:blue;">string</span>.IsNullOrEmpty(m_appPool)) { <span style="color:blue;">throw new </span><span style="color:#2b91af;">Exception</span>(<span style="color:#a31515;">"Property [AppPool] can't be null or empty"</span>); }
            <span style="color:blue;">if </span>(<span style="color:blue;">string</span>.IsNullOrEmpty(m_binding)) { <span style="color:blue;">throw new </span><span style="color:#2b91af;">Exception</span>(<span style="color:#a31515;">"Parameter [Binding] can't be null or empty"</span>); }
            <span style="color:blue;">if </span>(<span style="color:blue;">string</span>.IsNullOrEmpty(m_server)) { <span style="color:blue;">throw new </span><span style="color:#2b91af;">Exception</span>(<span style="color:#a31515;">"Parameter [Server] can't be null or empty"</span>); }
            <span style="color:blue;">if </span>(<span style="color:blue;">string</span>.IsNullOrEmpty(m_webFolder)) { <span style="color:blue;">throw new </span><span style="color:#2b91af;">Exception</span>(<span style="color:#a31515;">"Parameter [WebFolder] can't be null or empty"</span>); }
            <span style="color:blue;">if </span>(<span style="color:blue;">string</span>.IsNullOrEmpty(m_websiteName)) { <span style="color:blue;">throw new </span><span style="color:#2b91af;">Exception</span>(<span style="color:#a31515;">"Parameter [WebsiteName] can't be null or empty"</span>); }
            <span style="color:blue;">int </span>websiteId = 1;

            <span style="color:blue;">using </span>(<span style="color:#2b91af;">DirectoryEntry </span>w3svc = <span style="color:blue;">new </span><span style="color:#2b91af;">DirectoryEntry</span>(<span style="color:blue;">string</span>.Format(<span style="color:#a31515;">"IIS://{0}/w3svc"</span>, m_server)))
            {
                w3svc.RefreshCache();

                websiteId = <span style="color:blue;">this</span>.GetWebSiteId(m_server, m_websiteName);

                <span style="color:blue;">if </span>(websiteId &lt; 0)
                {
                    <span style="color:green;">//Create a website object array
                    </span><span style="color:blue;">object</span>[] newsite = <span style="color:blue;">new object</span>[] { m_websiteName, <span style="color:blue;">new object</span>[] { m_binding }, m_webFolder };

                    <span style="color:green;">//invoke IIsWebService.CreateNewSite
                    </span>websiteId = (<span style="color:blue;">int</span>)w3svc.Invoke(<span style="color:#a31515;">"CreateNewSite"</span>, newsite);

                    <span style="color:green;">// get newly created object
                    </span><span style="color:blue;">using </span>(<span style="color:#2b91af;">DirectoryEntry </span>website = <span style="color:blue;">new </span><span style="color:#2b91af;">DirectoryEntry</span>(<span style="color:blue;">string</span>.Format(<span style="color:#a31515;">"IIS://{0}/w3svc/{1}"</span>, m_server, websiteId)))
                    {
                        website.RefreshCache();
                        <span style="color:green;">// upgrade Scriptmap to 2.0.50272 (ASP.NET version)
                        </span><span style="color:blue;">for </span>(<span style="color:blue;">int </span>prop = 0; prop &lt; website.Properties[<span style="color:#a31515;">"ScriptMaps"</span>].Count; prop++)
                        {
                            website.Properties[<span style="color:#a31515;">"ScriptMaps"</span>][prop] = website.Properties[<span style="color:#a31515;">"ScriptMaps"</span>][prop].ToString().Replace(<span style="color:#a31515;">"v1.1.4322"</span>, <span style="color:#a31515;">"v2.0.50727"</span>);
                        }

                        <span style="color:green;">// set application pool
                        </span>website.Properties[<span style="color:#a31515;">"AppPoolId"</span>][0] = m_appPool;

                        <span style="color:green;">// set Execute Permissions (0 - Scripts only, 512 - Script Only, 516 Script and Execute
                        </span>website.Properties[<span style="color:#a31515;">"AccessFlags"</span>][0] = 512;

                        <span style="color:green;">// set ReadAccess
                        </span>website.Properties[<span style="color:#a31515;">"AccessRead"</span>][0] = <span style="color:blue;">true</span>;

                        <span style="color:green;">//// set Application Name (friendly name)
                        //// doesn't seem to work...
                        //w3svc.Properties["AppFriendlyName"][0] = siteDescription;

                        // Set Directory Security (Integrated Windows Authentication) 1 = AuthAnonymous, 2 = AuthBasic, 4 =AuthNTLM, 16 = AuthMD5(Digest), 64 = AuthPassport
                        </span>website.Properties[<span style="color:#a31515;">"AuthFlags"</span>][0] = 5;

                        <span style="color:green;">// save properties to IIS-metabase
                        </span>website.CommitChanges();

                        <span style="color:green;">// start website
                        </span>website.Invoke(<span style="color:#a31515;">"Start"</span>, <span style="color:blue;">null</span>);
                    }
                }
                <span style="color:blue;">else
                </span>{
                    websiteId = 0;
                }
            }

            <span style="color:blue;">return </span>websiteId;
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
            <span style="color:blue;">if </span>(<span style="color:blue;">string</span>.IsNullOrEmpty(serverName)) { <span style="color:blue;">throw new </span><span style="color:#2b91af;">Exception</span>(<span style="color:#a31515;">"Parameter [serverName] can't be null or empty"</span>); }
            <span style="color:blue;">if </span>(<span style="color:blue;">string</span>.IsNullOrEmpty(websiteName)) { <span style="color:blue;">throw new </span><span style="color:#2b91af;">Exception</span>(<span style="color:#a31515;">"Parameter [websiteName] can't be null or empty"</span>); }
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

            <span style="color:blue;">return </span>result;
        }
    }
}
</pre><a href="http://11011.net/software/vspaste"></a><a href="http://11011.net/software/vspaste"></a>
---
ID: 548
post_title: 'How to programmatically configure Scripts Only or Scripts and Executable (setting the AccessFlags) in IIS 7 with C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/06/12/how-to-programmatically-configure-scripts-only-or-scripts-and-executable-setting-the-accessflags-in-iis-7-with-c/
published: true
post_date: 2009-06-12 16:20:53
---
<p>In IIS 6 you could create a virtual directory with execute permissions, see code below, but running the code on IIS 7 would not set the AccessFalgs found at&quot;:    <br />&gt; start &gt; run &gt; inetmgr &gt; servername &gt; Sites &gt; SiteName &gt; Click on Handler Mappings &gt; Edit Feature Permissions &gt;     <br />    <br />    <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/06/image3.png"><img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/06/image-thumb3.png" width="244" height="156" /></a>     <br /></p>  <p>You should run the code below, but this would not set the accessflags, these should be set using the web.config of you’re ASP .NET 3.5 application:    <br />    <br /></p>  <pre class="code"><span style="color: blue">&lt;</span><span style="color: #a31515">configuration</span><span style="color: blue">&gt;
  &lt;</span><span style="color: #a31515">system.webServer</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">handlers </span><span style="color: red">accessPolicy</span><span style="color: blue">=</span>&quot;<span style="color: blue">Read, Execute, Script</span>&quot;<span style="color: blue">&gt;</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>If not set in the web.config the virtual directory will inherit the settings from the parent website
  <br />In this way you can create a virtual directory for a ASP .NET 3.5 application that works on IIS 6 and IIS 7

  <br />

  <br /><strong>Code
    <br /></strong>

  <br />

  <br /></p>

<pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.ComponentModel;
<span style="color: blue">using </span>System.Data;
<span style="color: blue">using </span>System.DirectoryServices;
<span style="color: blue">using </span>System.Drawing;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Text;
<span style="color: blue">using </span>System.Windows.Forms;

<span style="color: blue">namespace </span>WindowsFormsApplication1
{
    <span style="color: blue">public partial class </span><span style="color: #2b91af">Form1 </span>: <span style="color: #2b91af">Form
    </span>{
        <span style="color: blue">public string </span>VirDirSchemaName = <span style="color: #a31515">&quot;IIsWebVirtualDir&quot;</span>;

         <span style="color: blue">private string </span>m_server;
        <span style="color: blue">public string </span>Server
        {
            <span style="color: blue">get </span>{ <span style="color: blue">return </span>m_server; }
            <span style="color: blue">set </span>{ m_server = <span style="color: blue">value</span>; }
        }

        <span style="color: blue">private string </span>m_virtualDirectoryName;
        <span style="color: blue">public string </span>VirtualDirectoryName
        {
            <span style="color: blue">get </span>{ <span style="color: blue">return </span>m_virtualDirectoryName; }
            <span style="color: blue">set </span>{ m_virtualDirectoryName = <span style="color: blue">value</span>; }
        }

        <span style="color: blue">private string </span>m_virtualDirectoryFolder;
        <span style="color: blue">public string </span>VirtualDirectoryFolder
        {
            <span style="color: blue">get </span>{ <span style="color: blue">return </span>m_virtualDirectoryFolder; }
            <span style="color: blue">set </span>{ m_virtualDirectoryFolder = <span style="color: blue">value</span>; }
        }

        <span style="color: blue">private string </span>m_websiteName;
        <span style="color: blue">public string </span>WebsiteName
        {
            <span style="color: blue">get </span>{ <span style="color: blue">return </span>m_websiteName; }
            <span style="color: blue">set </span>{ m_websiteName = <span style="color: blue">value</span>; }
        }

        <span style="color: blue">private string </span>m_appPoolId;
        <span style="color: blue">public string </span>AppPoolId
        {
            <span style="color: blue">get </span>{ <span style="color: blue">return </span>m_appPoolId; }
            <span style="color: blue">set </span>{ m_appPoolId = <span style="color: blue">value</span>; }
        }

        <span style="color: blue">public </span>Form1()
        {
            InitializeComponent();
        }

        <span style="color: blue">private void </span>button1_Click(<span style="color: blue">object </span>sender, <span style="color: #2b91af">EventArgs </span>e)
        {

            <span style="color: blue">this</span>.Server = <span style="color: #a31515">&quot;localhost&quot;</span>;
            <span style="color: blue">this</span>.VirtualDirectoryName = <span style="color: #a31515">&quot;TestVd11&quot;</span>;
            <span style="color: blue">this</span>.VirtualDirectoryFolder = <span style="color: #a31515">@&quot;C:\Temp&quot;</span>;
            <span style="color: blue">this</span>.WebsiteName = <span style="color: #a31515">&quot;Test&quot;</span>;
            <span style="color: blue">this</span>.AppPoolId = <span style="color: #a31515">&quot;TestAppPool&quot;</span>;
            <span style="color: blue">this</span>.CreateVirtualDirectory();
        }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Create an IIS virtualdirectory
        </span><span style="color: gray">/// &lt;/summary&gt;
        </span><span style="color: blue">public void </span>CreateVirtualDirectory()
        {

            <span style="color: blue">int </span>websiteId = <span style="color: blue">this</span>.GetWebSiteId(m_server, m_websiteName);

            <span style="color: blue">try
            </span>{
                <span style="color: blue">using </span>(<span style="color: #2b91af">DirectoryEntry </span>w3svc = <span style="color: blue">new </span><span style="color: #2b91af">DirectoryEntry</span>(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;IIS://{0}/w3svc/{1}&quot;</span>, m_server, websiteId)))
                {
                    w3svc.RefreshCache();

                    <span style="color: blue">foreach </span>(<span style="color: #2b91af">DirectoryEntry </span>child <span style="color: blue">in </span>w3svc.Children)
                    {
                        <span style="color: blue">using </span>(child)
                        {
                            child.RefreshCache();

                            <span style="color: blue">if </span>(child.Name.Equals(<span style="color: #a31515">&quot;root&quot;</span>, <span style="color: #2b91af">StringComparison</span>.OrdinalIgnoreCase))
                            {
                                <span style="color: green">// Remove virtual directory if it exists.
                                </span><span style="color: #2b91af">DirectoryEntry </span>vd = <span style="color: blue">null</span>;
                                <span style="color: blue">try
                                </span>{
                                    vd = child.Children.Find(m_virtualDirectoryName, VirDirSchemaName);
                                    <span style="color: blue">if </span>(vd != <span style="color: blue">null</span>)
                                    {
                                        vd.Invoke(<span style="color: #a31515">&quot;AppDelete&quot;</span>);
                                        child.Children.Remove(vd);
                                        child.CommitChanges();
                                    }
                                }
                                <span style="color: blue">catch
                                </span>{
                                }
                                <span style="color: blue">finally
                                </span>{
                                    <span style="color: blue">if </span>(vd != <span style="color: blue">null</span>)
                                        vd.Dispose();
                                }

                                <span style="color: blue">using </span>(<span style="color: #2b91af">DirectoryEntry </span>newVirDir = (<span style="color: #2b91af">DirectoryEntry</span>) child.Invoke(<span style="color: #a31515">&quot;Create&quot;</span>, <span style="color: #a31515">&quot;IIsWebVirtualDir&quot;</span>, m_virtualDirectoryName))
                                {
                                    newVirDir.Properties[<span style="color: #a31515">&quot;AccessRead&quot;</span>][0] = <span style="color: blue">true</span>;
                                    newVirDir.Properties[<span style="color: #a31515">&quot;AccessScript&quot;</span>][0] = <span style="color: blue">true</span>;
                                    newVirDir.Properties[<span style="color: #a31515">&quot;AccessExecute&quot;</span>][0] = <span style="color: blue">true</span>;
                                    newVirDir.Properties[<span style="color: #a31515">&quot;AppPoolId&quot;</span>][0] = <span style="color: blue">this</span>.AppPoolId;
                                    newVirDir.InvokeSet(<span style="color: #a31515">&quot;Path&quot;</span>, m_virtualDirectoryFolder.Trim(<span style="color: #a31515">'/'</span>));
                                    newVirDir.Invoke(<span style="color: #a31515">&quot;AppCreate&quot;</span>, <span style="color: blue">true</span>);
                                    newVirDir.InvokeSet(<span style="color: #a31515">&quot;AppFriendlyName&quot;</span>, m_virtualDirectoryName);
                                    newVirDir.CommitChanges();
                                }
                            }

                            child.CommitChanges();
                        }
                    }

                    w3svc.CommitChanges();
                }
            }
            <span style="color: blue">catch </span>(<span style="color: #2b91af">Exception </span>ex)
            {
                <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;Virtual Directory [{0}] already exists or error during creation. [{1}]&quot;</span>, m_virtualDirectoryName, ex.ToString()));
            }
        }

        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Get website id on websitename
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;serverName&quot;&gt;</span><span style="color: green">Name of the IIS server e.g. localhost, can be a netbios name, but can't be a host header</span><span style="color: gray">&lt;/param&gt;
        /// &lt;param name=&quot;websiteName&quot;&gt;</span><span style="color: green">Name of the website e.g. test</span><span style="color: gray">&lt;/param&gt;
        /// &lt;returns&gt;
        /// </span><span style="color: green">Less the 0, site does not exist
        </span><span style="color: gray">/// </span><span style="color: green">Id of the existing site
        </span><span style="color: gray">/// &lt;/returns&gt;
        </span><span style="color: blue">public int </span>GetWebSiteId(<span style="color: blue">string </span>serverName, <span style="color: blue">string </span>websiteName)
        {
            <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(serverName)) { <span style="color: blue">throw new </span><span style="color: #2b91af">Exception</span>(<span style="color: #a31515">&quot;Parameter [serverName] can't be null or empty&quot;</span>); } <span style="color: blue">else </span>{ <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;GetWebSiteId: [{0}]&quot;</span>, serverName)); }
            <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(websiteName)) { <span style="color: blue">throw new </span><span style="color: #2b91af">Exception</span>(<span style="color: #a31515">&quot;Parameter [websiteName] can't be null or empty&quot;</span>); } <span style="color: blue">else </span>{ <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;GetWebSiteId: [{0}]&quot;</span>, websiteName)); }
            <span style="color: blue">int </span>result = -1;

            <span style="color: blue">using </span>(<span style="color: #2b91af">DirectoryEntry </span>w3svc = <span style="color: blue">new </span><span style="color: #2b91af">DirectoryEntry</span>(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;IIS://{0}/w3svc&quot;</span>, serverName)))
            {
                w3svc.RefreshCache();

                <span style="color: blue">foreach </span>(<span style="color: #2b91af">DirectoryEntry </span>site <span style="color: blue">in </span>w3svc.Children)
                {
                    <span style="color: blue">using </span>(site)
                    {
                        site.RefreshCache();

                        <span style="color: blue">if </span>(site.Properties[<span style="color: #a31515">&quot;ServerComment&quot;</span>] != <span style="color: blue">null</span>)
                        {
                            <span style="color: blue">if </span>(site.Properties[<span style="color: #a31515">&quot;ServerComment&quot;</span>].Value != <span style="color: blue">null</span>)
                            {
                                <span style="color: blue">if </span>(site.Properties[<span style="color: #a31515">&quot;ServerComment&quot;</span>].Value.ToString().Equals(websiteName, <span style="color: #2b91af">StringComparison</span>.OrdinalIgnoreCase))
                                {
                                    result = <span style="color: blue">int</span>.Parse(site.Name);
                                }
                            }
                        }
                    }
                }
            }

            <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;GetWebSiteId: [{0}]&quot;</span>, result));
            <span style="color: blue">return </span>result;
        }
    }
}</pre>
<a href="http://11011.net/software/vspaste"></a>
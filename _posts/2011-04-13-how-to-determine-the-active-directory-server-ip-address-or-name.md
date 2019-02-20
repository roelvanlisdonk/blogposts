---
ID: 1975
post_title: >
  How to determine the active directory
  server IP address or name
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/04/13/how-to-determine-the-active-directory-server-ip-address-or-name/
published: true
post_date: 2011-04-13 11:40:09
---
<p>If you logon to a domain you can get the IP address of the active directory server by executing the following steps:</p>  <p>start &gt; cmd &gt; echo %LOGONSERVER%</p>  <p>&#160;</p>  <p>You could also try to ping you’re domain:</p>  <p>start &gt; cmd &gt; ping mydomain.local</p>  <p>&#160;</p>  <p>If you want to determine the domain controller name in C#, use:</p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Text;
<span style="color: blue">using </span>System.DirectoryServices.AccountManagement;

<span style="color: blue">namespace </span>ConsoleApplication1
{
    <span style="color: blue">class </span><span style="color: #2b91af">Program
    </span>{
        <span style="color: blue">static void </span>Main(<span style="color: blue">string</span>[] args)
        {
            <span style="color: blue">using </span>(<span style="color: #2b91af">PrincipalContext </span>context = <span style="color: blue">new </span><span style="color: #2b91af">PrincipalContext</span>(<span style="color: #2b91af">ContextType</span>.Domain))
            {
                <span style="color: blue">string </span>controller = context.ConnectedServer;
                <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;Domain Controller: {0}&quot;</span>, controller));
                <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: #a31515">&quot;Press any key to exit.&quot;</span>);
                <span style="color: #2b91af">Console</span>.ReadLine();
            }
        }
    }
}</pre>

<p><strong>Result</strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/04/image2.png"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/04/image_thumb2.png" width="648" height="170" /></a></p>
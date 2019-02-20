---
ID: 1736
post_title: 'How to run an existing SQL Server Agent Job from C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/09/23/how-to-run-an-existing-sql-server-agent-job-from-c/
published: true
post_date: 2010-09-23 13:18:12
---
<p>If you want to execute an existing Microsoft SQL Server Agent Job in C# you an use the following function:   <br />    <br />The function uses SQL authentication to connect to the Microsoft SQL Server instance.    <br /></p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Text;
<span style="color: blue">using </span>Microsoft.SqlServer.Management.Smo;
<span style="color: blue">using </span>Microsoft.SqlServer.Management.Smo.Agent;
<span style="color: blue">using </span>Microsoft.SqlServer.Management.Common;
<span style="color: blue">using </span>System.Data;</pre>

<p>&#160;</p>

<pre class="code"><span style="color: blue">public override void </span>Execute()
    {
      <span style="color: #2b91af">Server </span>server = <span style="color: blue">new </span><span style="color: #2b91af">Server</span>(@&quot;MyServer\MyInstanceName&quot;);
      <span style="color: blue">try
      </span>{
        server.ConnectionContext.LoginSecure = <span style="color: blue">false</span>;
        server.ConnectionContext.Login = &quot;<span style="color: #2b91af">MyName&quot;</span>;
        server.ConnectionContext.Password = &quot;MyPassword&quot;;
        server.ConnectionContext.Connect();
        <span style="color: #2b91af">Job </span>job = server.JobServer.Jobs[Name];
        job.Start();
      }
      <span style="color: blue">finally
      </span>{
        <span style="color: blue">if </span>(server.ConnectionContext.IsOpen)
        {
          server.ConnectionContext.Disconnect();
        }
          
      }
    }</pre>
<a href="http://11011.net/software/vspaste"></a>
---
ID: 1658
post_title: 'How to determine if an ApplicationPool exists in IIS7 with C# and LINQ'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/08/10/how-to-determine-if-an-applicationpool-exists-in-iis7-with-c-and-linq/
published: true
post_date: 2010-08-10 09:43:05
---
<p>If you want to determine if an ApplicationPool exists in IIS7 you can use the following code:</p>  <pre class="code"><span style="color: blue">        public bool </span>Exists(<span style="color: blue">string </span>name)
        {
            <span style="color: blue">bool </span>result = <span style="color: blue">false</span>;

            <span style="color: blue">using </span>(<span style="color: #2b91af">ServerManager </span>manager = <span style="color: blue">new </span><span style="color: #2b91af">ServerManager</span>())
            {
                result = manager.ApplicationPools.Any(t =&gt; t.Name == name);
            }

            <span style="color: blue">return </span>result;
        }</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>You can find the Microsoft.Web.Administration.dll in &quot;%windir%\System32\inetsrv&quot;.</p>
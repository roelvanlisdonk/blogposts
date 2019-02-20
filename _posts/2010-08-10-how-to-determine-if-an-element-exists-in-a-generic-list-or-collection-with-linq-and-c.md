---
ID: 1659
post_title: 'How to determine if an element exists in a generic list or collection with LINQ and C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/08/10/how-to-determine-if-an-element-exists-in-a-generic-list-or-collection-with-linq-and-c/
published: true
post_date: 2010-08-10 15:08:34
---
<p>If you want to determine if an element in a generic list or collection exists, use the &quot;Any&quot; function with a lambda expression, like:</p>  <pre class="code"><span style="color: blue">        public bool </span>Exists(<span style="color: blue">string </span>name)
        {
            <span style="color: blue">bool </span>result = <span style="color: blue">false</span>;

            <span style="color: blue">using </span>(<span style="color: #2b91af">ServerManager </span>manager = <span style="color: blue">new </span><span style="color: #2b91af">ServerManager</span>())
            {
                result = manager.ApplicationPools.Any(a =&gt; a.Name == name);
            }

            <span style="color: blue">return </span>result;
        }</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>You can find the Microsoft.Web.Administration.dll in &quot;%windir%\System32\inetsrv&quot;.</p>
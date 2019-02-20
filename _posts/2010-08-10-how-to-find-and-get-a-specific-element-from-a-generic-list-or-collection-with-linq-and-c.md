---
ID: 1660
post_title: 'How to find and get a specific element from a generic list or collection with LINQ and C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/08/10/how-to-find-and-get-a-specific-element-from-a-generic-list-or-collection-with-linq-and-c/
published: true
post_date: 2010-08-10 15:13:09
---
<p align="left">If you want to find or get an element from a generic list or collection with LINQ and C#, you can use the &quot;First&quot; function:</p>  <pre class="code"><span style="color: blue">public </span><span style="color: #2b91af">ApplicationPool </span>GetApplicationPoolByName(<span style="color: blue">string </span>name)
{
    <span style="color: #2b91af">ApplicationPool </span>applicationPool;
    <span style="color: blue">using </span>(<span style="color: #2b91af">ServerManager </span>manager = <span style="color: blue">new </span><span style="color: #2b91af">ServerManager</span>())
    {
        applicationPool = manager.ApplicationPools.First(a =&gt; a.Name == name);
    }

    <span style="color: blue">return </span>applicationPool;
}</pre>
<a href="http://11011.net/software/vspaste"></a>

<div align="left">&#160;</div>

<div align="left">&#160;</div>
<a href="http://11011.net/software/vspaste"></a>

<p align="left">You can find the Microsoft.Web.Administration.dll in &quot;%windir%\System32\inetsrv&quot;.</p>
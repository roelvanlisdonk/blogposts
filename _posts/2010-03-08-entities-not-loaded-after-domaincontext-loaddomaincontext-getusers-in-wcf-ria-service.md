---
ID: 1077
post_title: >
  Entities not loaded after
  domainContext.Load(domainContext.GetUsers)
  in WCF RIA service
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/08/entities-not-loaded-after-domaincontext-loaddomaincontext-getusers-in-wcf-ria-service/
published: true
post_date: 2010-03-08 14:51:09
---
<p>If you use LINQ to SQL and you’re entities are not loaded after you call a GetQuery on the DomainContext, you probably did not use a callback.</p>  <blockquote>   <pre class="code"><span style="color: #2b91af">TTSDomainContext </span>context = <span style="color: blue">new </span><span style="color: #2b91af">TTSDomainContext</span>();
<span style="color: #2b91af">LoadOperation </span>op = context.Load(
context.GetTasksQuery(),
<font size="4">result =&gt;
{
  <span style="color: blue">if </span>(!result.HasError)
  {
    <span style="color: blue">//At this point the entities are loaded</span></font></pre>
</blockquote>

<pre class="code"><span style="color: blue"></span><font size="4">       }</font>
    },<span style="color: blue">null</span>); </pre>
<a href="http://11011.net/software/vspaste"></a><a href="http://11011.net/software/vspaste"></a>
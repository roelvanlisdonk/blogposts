---
ID: 2213
post_title: >
  How to set the connectionstring at
  runtime of a dbcontext in Entity
  Framework 4.2
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/11/15/how-to-set-the-connectionstring-at-runtime-of-a-dbcontext-in-entity-framework-4-2/
published: true
post_date: 2011-11-15 16:20:02
---
<p>If you want to set the connectionstring for a dbcontext, when using EntityFramework 4.2, just create a partial class for the specific dbcontext and add a constructor that call’s de dbcontext constructor with connectionstring. Now you can instantiate MyDatabaseEntities with a connectionstring.</p>  <p>&#160;</p>  <pre class="code"><span style="color: blue">public partial class </span><span style="color: #2b91af">MyDatabaseEntities
    </span>{
        <span style="color: blue">public </span>MyDatabaseEntities(<span style="color: blue">string </span>connection)
            : <span style="color: blue">base</span>(connection)
        {
        }
    }</pre>


<p>The generated partial class looks something like:</p>

<p>&#160;</p>

<pre class="code"><span style="color: blue">public partial class </span><span style="color: #2b91af">MyDatabaseEntities </span>: <span style="color: #2b91af">DbContext
    </span>{
        <span style="color: blue">public </span>MyDatabaseEntities()
            : <span style="color: blue">base</span>(<span style="color: #a31515">&quot;name=MyDatabaseEntities&quot;</span>)
        {
        }
    
        <span style="color: blue">protected override void </span>OnModelCreating(<span style="color: #2b91af">DbModelBuilder </span>modelBuilder)
        {
            <span style="color: blue">throw new </span><span style="color: #2b91af">UnintentionalCodeFirstException</span>();
        }
    
        <span style="color: blue">public </span><span style="color: #2b91af">DbSet</span>&lt;<span style="color: #2b91af">Products</span>&gt; Products { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }

    }</pre>
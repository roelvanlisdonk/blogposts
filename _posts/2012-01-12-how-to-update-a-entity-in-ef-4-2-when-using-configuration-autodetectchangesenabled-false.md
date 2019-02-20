---
ID: 2461
post_title: >
  How to update a entity in EF 4.2, when
  using
  Configuration.AutoDetectChangesEnabled =
  false.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/01/12/how-to-update-a-entity-in-ef-4-2-when-using-configuration-autodetectchangesenabled-false/
published: true
post_date: 2012-01-12 15:58:28
---
<p>&#160;</p>  <p>When you use DbContext.Configuration.AutoDetectChangesEnabled = false to improve performance, then there will be no automatically state tracking (this is what’s causing the performance penalty). To update a entity in the database, including it’s releated entities (navgiation properties), you should use the Entry function on the DbContext:</p>  <pre class="code"><span style="color: blue">using </span>System.Data.Entity;
<span style="color: blue">using </span>System.Linq;</pre>

<pre class="code">[<span style="color: #2b91af">TestMethod</span>]
<span style="color: blue">public void </span>TestChangeTrackingEF()
{
    <span style="color: blue">using </span>(<span style="color: blue">var </span>entities = <span style="color: blue">new </span><span style="color: #2b91af">MyEntities</span>())
    {
        <span style="color: green">// Set Configuration.AutoDetectChangesEnabled = false to improve performance (100x).
        </span>entities.Configuration.AutoDetectChangesEnabled = <span style="color: blue">false</span>;

        <span style="color: green">// By default use lazyloading.
        </span>entities.Configuration.LazyLoadingEnabled = <span style="color: blue">true</span>; 

        <span style="color: green">// Get a specific entity from the database
        </span><span style="color: blue">var </span>query = <span style="color: blue">from </span>i <span style="color: blue">in </span>entities.ImageInfo
                    <span style="color: blue">where </span>i.Id == 41
                    <span style="color: blue">select </span>i;
        <span style="color: #2b91af">ImageInfo </span>info = query.First();

        <span style="color: green">// Update the entity
        </span>info.ProcessStatusId = 9;
                
        <span style="color: green">// Set state to Modified
        </span>entities.Entry(info).State = System.Data.<span style="color: #2b91af">EntityState</span>.Modified;

        <span style="color: green">// Save changes to the database.
        </span>entities.SaveChanges();
    }
}</pre>

<p><strong>NOTE</strong></p>

<p>Setting the state to EntityState.Modified will update all columns of the object (because change tracking is disabled).</p>

<p>If you only want to update a specific column, for example you know which columns are dirty, then you can use the <strong>IsModified</strong> property of a <strong>DbPropertyEntry</strong> object, this object can be obtained by using the <strong>Entity.Property()</strong> method:</p>

<pre>entities.Entry(info).Property(&quot;Description&quot;).IsModified = true;</pre>
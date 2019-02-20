---
ID: 2827
post_title: >
  How to make Entity Framework 5.0 use an
  in-memory persistence DbContext instead
  of accessing the database.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/08/23/how-to-make-entity-framework-5-0-use-an-in-memory-persistence-dbcontext-instead-of-accessing-the-database/
published: true
post_date: 2012-08-23 23:00:53
---
<p>If you want to switch between in-memory stub data and a database during runtime with Entity Framework 5.0, you have several options, some of them are:</p>  <p>- Using a second level cache mechanism like <a href="http://www.codeproject.com/Articles/435142/Entity-Framework-Second-Level-Caching-with-DbConte">http://www.codeproject.com/Articles/435142/Entity-Framework-Second-Level-Caching-with-DbConte</a> , filling the cache before use and setting the expiration time to infinite.</p>  <p>- Creating a extension method on the DbSet class that uses only the DbSet (for direct database access) or DbSet.Local for in-memory stub data, based on some parameter.</p>  <p>- Implement a MemoryPersistenceDbContext and MemoryPersistenceDbSet.</p>  <p>&#160;</p>  <p>This post will focus on the last option.</p>  <p><strong>Create a new MVC4 project in Microsoft Visual Studio 2010</strong></p>  <p>File &gt; New &gt; Project</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image_thumb.png" width="538" height="65" /></a></p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image1.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image_thumb1.png" width="580" height="405" /></a></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image2.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image_thumb2.png" width="580" height="527" /></a></p>  <p>&#160;</p>  <p><strong>Add Entity Framework 5.0 NuGet package</strong></p>  <p>Rightclick solution &gt; Manage NuGet Packages for Solution…</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image3.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image_thumb3.png" width="580" height="237" /></a></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image4.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image_thumb4.png" width="580" height="390" /></a></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image5.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image_thumb5.png" width="366" height="364" /></a></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image6.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image_thumb6.png" width="370" height="412" /></a></p>  <p>&#160;</p>  <p><strong>I added 2 tables to a Research database on a LocalDb SQL Server 2012 instance</strong> </p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image7.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image_thumb7.png" width="429" height="506" /></a></p>  <p><strong>Add *.edmx model</strong></p>  <p>Right click on the models folder:</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image8.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image_thumb8.png" width="490" height="366" /></a></p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image9.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image_thumb9.png" width="580" height="402" /></a></p>  <p>ModelName = ResearchModel.edmx</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image10.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image_thumb10.png" width="468" height="416" /></a></p>  <p>DbContext name = ResearchUow</p>  <p>(UOW = Unit of work)</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image11.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image_thumb11.png" width="536" height="478" /></a></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image12.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image_thumb12.png" width="551" height="496" /></a></p>  <p>Model namespace = ResearchModel</p>  <p>Check all tables</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image13.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image_thumb13.png" width="580" height="518" /></a></p>  <p><strong>Add code generation item</strong></p>  <p>Open the ResearchUow.edmx &gt; right click &gt; Add Code Generation Item…</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image14.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image_thumb14.png" width="377" height="361" /></a></p>  <p>Code generation item name = ResearchModel.tt</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image15.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image_thumb15.png" width="580" height="402" /></a></p>  <p>Now the project looks like</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image16.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image_thumb16.png" width="302" height="498" /></a></p>  <p>&#160;</p>  <p><strong>Add an IEntity interface</strong></p>  <p>This interface will be used to make the Find function work.</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image17.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image_thumb17.png" width="580" height="405" /></a></p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Text;

<span style="color: blue">namespace </span>Mvc4Application.Models
{
    <span style="color: blue">public interface </span><span style="color: #2b91af">IEntity
    </span>{
        <span style="color: blue">int </span>Id { <span style="color: blue">get</span>; }
    }
}</pre>


<p><strong>Add a MemoryPersistenceDbSet.cs in the Models folder</strong></p>

<p>This will be used to store the data in-memory instead of in the database.</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image18.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image_thumb18.png" width="580" height="405" /></a></p>


<pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Collections.ObjectModel;
<span style="color: blue">using </span>System.Data.Entity;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Linq.Expressions;

<span style="color: blue">namespace </span>Mvc4Application.Models
{
    <span style="color: blue">public class </span><span style="color: #2b91af">MemoryPersistenceDbSet</span>&lt;T&gt; : <span style="color: #2b91af">IDbSet</span>&lt;T&gt; <span style="color: blue">where </span>T : <span style="color: blue">class
    </span>{
        <span style="color: #2b91af">ObservableCollection</span>&lt;T&gt; _data;
        <span style="color: #2b91af">IQueryable </span>_query;

        <span style="color: blue">public </span>MemoryPersistenceDbSet()
        {
            _data = <span style="color: blue">new </span><span style="color: #2b91af">ObservableCollection</span>&lt;T&gt;();
            _query = _data.AsQueryable();
        }
        <span style="color: blue">public virtual </span>T Find(<span style="color: blue">params object</span>[] keyValues)
        {
            <span style="color: blue">if </span>(!(<span style="color: blue">typeof</span>(T) <span style="color: blue">is </span><span style="color: #2b91af">IEntity</span>)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentException</span>(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;Entity [{0}] does not contain a property [Id], so it could not be converted to the IEntity interface, used in this function.&quot;</span>, <span style="color: blue">typeof</span>(T).ToString())); }
            <span style="color: blue">return this</span>.SingleOrDefault(e =&gt; (e <span style="color: blue">as </span><span style="color: #2b91af">IEntity</span>).Id == (<span style="color: blue">int</span>)keyValues.Single());
        }
        <span style="color: blue">public </span>T Add(T item)
        {
            _data.Add(item);
            <span style="color: blue">return </span>item;
        }
        <span style="color: blue">public </span>T Remove(T item)
        {
            _data.Remove(item);
            <span style="color: blue">return </span>item;
        }
        <span style="color: blue">public </span>T Attach(T item)
        {
            _data.Add(item);
            <span style="color: blue">return </span>item;
        }
        <span style="color: blue">public </span>T Detach(T item)
        {
            _data.Remove(item);
            <span style="color: blue">return </span>item;
        }
        <span style="color: blue">public </span>T Create()
        {
            <span style="color: blue">return </span><span style="color: #2b91af">Activator</span>.CreateInstance&lt;T&gt;();
        }
        <span style="color: blue">public </span>TDerivedEntity Create&lt;TDerivedEntity&gt;() <span style="color: blue">where </span>TDerivedEntity : <span style="color: blue">class</span>, T
        {
            <span style="color: blue">return </span><span style="color: #2b91af">Activator</span>.CreateInstance&lt;TDerivedEntity&gt;();
        }
        <span style="color: blue">public </span><span style="color: #2b91af">ObservableCollection</span>&lt;T&gt; Local
        {
            <span style="color: blue">get </span>{ <span style="color: blue">return </span>_data; }
        }
        <span style="color: #2b91af">Type IQueryable</span>.ElementType
        {
            <span style="color: blue">get </span>{ <span style="color: blue">return </span>_query.ElementType; }
        }
        <span style="color: #2b91af">Expression IQueryable</span>.Expression
        {
            <span style="color: blue">get </span>{ <span style="color: blue">return </span>_query.Expression; }
        }
        <span style="color: #2b91af">IQueryProvider IQueryable</span>.Provider
        {
            <span style="color: blue">get </span>{ <span style="color: blue">return </span>_query.Provider; }
        }
        <span style="color: #2b91af">IEnumerator IEnumerable</span>.GetEnumerator()
        {
            <span style="color: blue">return </span>_data.GetEnumerator();
        }
        <span style="color: #2b91af">IEnumerator</span>&lt;T&gt; <span style="color: #2b91af">IEnumerable</span>&lt;T&gt;.GetEnumerator()
        {
            <span style="color: blue">return </span>_data.GetEnumerator();
        }
    }
}</pre>
<strong>Change the ResearchModel.tt file, so all generated POCO entities derive from IEntity</strong>

<p>Open the ResearchModel.tt files and change the line</p>

<p>&lt;#=codeStringGenerator.EntityClassOpening(entity)#&gt;
  <br />to

  <br />&lt;#=codeStringGenerator.EntityClassOpening(entity)#&gt; : IEntity</p>

<p>and click save, on save of the ResearchModel.tt file, the POCO entities will be regenerated and will now all implement the IEntity interface:</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image19.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image_thumb19.png" width="389" height="230" /></a></p>

<p>&#160;</p>

<p><strong>Change the ResearchModel.Context.tt file, so the IResearchUow interface, the ResearchUow class and the MemoryPersistenceResearchUow will be created.</strong></p>

<p>&#160;</p>

<p><strong><font color="#ff0000">Open the ResearchModel.Context.tt file and find the code:</font></strong></p>

<p>
  <br /><font size="1">&lt;#=Accessibility.ForType(container)#&gt; partial class &lt;#=code.Escape(container)#&gt; : DbContext
    <br />{

    <br />&#160;&#160;&#160; public &lt;#=code.Escape(container)#&gt;()

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; : base(&quot;name=&lt;#=container.Name#&gt;&quot;)

    <br />&#160;&#160;&#160; {

    <br />&lt;#

    <br />if (!loader.IsLazyLoadingEnabled(container))

    <br />{

    <br />#&gt;

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; this.Configuration.LazyLoadingEnabled = false;

    <br />&lt;#

    <br />}

    <br />#&gt;

    <br />&#160;&#160;&#160; }</font></p>

<p><font size="1">&#160;&#160;&#160; protected override void OnModelCreating(DbModelBuilder modelBuilder)
    <br />&#160;&#160;&#160; {

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; throw new UnintentionalCodeFirstException();

    <br />&#160;&#160;&#160; }</font></p>

<p><font size="1">&lt;#
    <br />&#160;&#160;&#160; foreach (var entitySet in container.BaseEntitySets.OfType&lt;EntitySet&gt;())

    <br />&#160;&#160;&#160; {

    <br />#&gt;

    <br />&#160;&#160;&#160; &lt;#=codeStringGenerator.DbSet(entitySet)#&gt;

    <br />&lt;#

    <br />&#160;&#160;&#160; }</font></p>

<p><font size="1">&#160;&#160;&#160; foreach (var edmFunction in container.FunctionImports)
    <br />&#160;&#160;&#160; {

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; WriteFunctionImport(typeMapper, codeStringGenerator, edmFunction, modelNamespace, includeMergeOption: false);

    <br />&#160;&#160;&#160; }

    <br />#&gt;

    <br />}

    <br />&lt;#</font></p>

<p><font size="1">if (!String.IsNullOrEmpty(codeNamespace))
    <br />{

    <br />&#160;&#160;&#160; PopIndent();

    <br />#&gt;

    <br />}

    <br />&lt;#

    <br />}

    <br />#&gt;</font></p>

<p>&#160;</p>

<p>&#160;</p>

<p><strong><font color="#ff0000">Replace by</font></strong></p>

<p>&#160;</p>

<p>
  <br /><font size="1">&lt;#=Accessibility.ForType(container)#&gt; partial interface <strong>IResearchlUow</strong>

    <br />{

    <br />&lt;#

    <br />&#160;&#160;&#160; foreach (var entitySet in container.BaseEntitySets.OfType&lt;EntitySet&gt;())

    <br />&#160;&#160;&#160; {

    <br />#&gt;

    <br />&#160;&#160;&#160; &lt;#=codeStringGenerator.IDbSet(entitySet)#&gt;

    <br />&lt;#

    <br />&#160;&#160;&#160; }</font></p>

<p><font size="1">&#160;&#160;&#160; foreach (var edmFunction in container.FunctionImports)
    <br />&#160;&#160;&#160; {

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; WriteFunctionImport(typeMapper, codeStringGenerator, edmFunction, modelNamespace, includeMergeOption: false);

    <br />&#160;&#160;&#160; }

    <br />#&gt;</font></p>

<p><font size="1">&#160;&#160;&#160; int SaveChanges();
    <br />}

    <br />&lt;#=Accessibility.ForType(container)#&gt; partial class &lt;#=code.Escape(container)#&gt; : DbContext, <strong>IResearchUow</strong>

    <br />{

    <br />&lt;#

    <br />&#160;&#160;&#160; foreach (var entitySet in container.BaseEntitySets.OfType&lt;EntitySet&gt;())

    <br />&#160;&#160;&#160; {

    <br />#&gt;

    <br />&#160;&#160;&#160; &lt;#=codeStringGenerator.DbSet(entitySet)#&gt;

    <br />&lt;#

    <br />&#160;&#160;&#160; }</font></p>

<p><font size="1">&#160;&#160;&#160; foreach (var edmFunction in container.FunctionImports)
    <br />&#160;&#160;&#160; {

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; WriteFunctionImport(typeMapper, codeStringGenerator, edmFunction, modelNamespace, includeMergeOption: false);

    <br />&#160;&#160;&#160; }

    <br />#&gt;</font></p>

<p><font size="1">&#160;&#160;&#160; public &lt;#=code.Escape(container)#&gt;() : base(&quot;name=&lt;#=container.Name#&gt;&quot;)
    <br />&#160;&#160;&#160; {

    <br />&lt;#

    <br />if (!loader.IsLazyLoadingEnabled(container))

    <br />{

    <br />#&gt;

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; this.Configuration.LazyLoadingEnabled = false;

    <br />&lt;#

    <br />}

    <br />#&gt;

    <br />&#160;&#160;&#160; }

    <br />&#160;&#160;&#160; public &lt;#=code.Escape(container)#&gt;(string connection) : base(connection)

    <br />&#160;&#160;&#160; {

    <br />&lt;#

    <br />if (!loader.IsLazyLoadingEnabled(container))

    <br />{

    <br />#&gt;

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; this.Configuration.LazyLoadingEnabled = false;

    <br />&lt;#

    <br />}

    <br />#&gt;

    <br />&#160;&#160;&#160; }

    <br />&#160;&#160;&#160; protected override void OnModelCreating(DbModelBuilder modelBuilder)

    <br />&#160;&#160;&#160; {

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; throw new UnintentionalCodeFirstException();

    <br />&#160;&#160;&#160; }

    <br />}

    <br />&lt;#=Accessibility.ForType(container)#&gt; partial class <strong>MemoryPersistenceResearchUow</strong> : &lt;#=code.Escape(container)#&gt;

    <br />{

    <br />&#160;&#160;&#160; public <strong>MemoryPersistenceResearchUow</strong>()

    <br />&#160;&#160;&#160; {

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; Seed();

    <br />&#160;&#160;&#160; }

    <br />&#160;&#160;&#160; public void ClearAll()

    <br />&#160;&#160;&#160; {

    <br />&lt;#

    <br />&#160;&#160;&#160; foreach (var entitySet in container.BaseEntitySets.OfType&lt;EntitySet&gt;())

    <br />&#160;&#160;&#160; {

    <br />#&gt;

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; &lt;#=codeStringGenerator.DbSetInConstructor(entitySet)#&gt;

    <br />&lt;#

    <br />&#160;&#160;&#160; }

    <br />#&gt;

    <br />&#160;&#160;&#160; }

    <br />&#160;&#160;&#160; public override int SaveChanges()

    <br />&#160;&#160;&#160; {

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; return 0;

    <br />&#160;&#160;&#160; }

    <br />}

    <br />&lt;#</font></p>

<p><font size="1">if (!String.IsNullOrEmpty(codeNamespace))
    <br />{

    <br />&#160;&#160;&#160; PopIndent();

    <br />#&gt;

    <br />}

    <br />&lt;#

    <br />}

    <br />#&gt;</font></p>

<p>&#160;</p>

<p><strong><font color="#ff0000">and find</font></strong></p>

<p><font size="1">public string DbSet(EntitySet entitySet)
    <br />{

    <br />&#160;&#160;&#160; return string.Format(

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; CultureInfo.InvariantCulture,

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; &quot;{0} DbSet&lt;{1}&gt; {2} {{ get; set; }}&quot;,

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; Accessibility.ForReadOnlyProperty(entitySet),

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; _typeMapper.GetTypeName(entitySet.ElementType),

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; _code.Escape(entitySet));

    <br />}

    <br /></font></p>

<p>&#160;</p>

<p><strong><font color="#ff0000">Replace by</font></strong></p>

<p>&#160;<font size="1">&#160;&#160; public string IDbSet(EntitySet entitySet)
    <br />&#160;&#160;&#160; {

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; return string.Format(

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; CultureInfo.InvariantCulture,

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &quot;IDbSet&lt;{0}&gt; {1} {{ get; set; }}&quot;,

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; _typeMapper.GetTypeName(entitySet.ElementType),

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; _code.Escape(entitySet));

    <br />&#160;&#160;&#160; }</font></p>

<p><font size="1">&#160;&#160;&#160; public string DbSet(EntitySet entitySet)
    <br />&#160;&#160;&#160; {

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; return string.Format(

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; CultureInfo.InvariantCulture,

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &quot;{0} IDbSet&lt;{1}&gt; {2} {{ get; set; }}&quot;,

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; Accessibility.ForReadOnlyProperty(entitySet),

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; _typeMapper.GetTypeName(entitySet.ElementType),

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; _code.Escape(entitySet));

    <br />&#160;&#160;&#160; }</font></p>

<p><font size="1">&#160;&#160;&#160; public string DbSetInConstructor(EntitySet entitySet)
    <br />&#160;&#160;&#160; {

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; return string.Format(

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; CultureInfo.InvariantCulture,

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &quot;this.{0} = new MemoryPersistenceDbSet&lt;{0}&gt;();&quot;,

    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; _typeMapper.GetTypeName(entitySet.ElementType));

    <br />&#160;&#160;&#160; }</font></p>

<p>&#160;</p>

<p>Now on save of the ResearchModel.Context.tt&#160; T4 template will generate the following code:</p>

<pre class="code"><span style="color: blue">namespace </span>Mvc4Application.Models
{
    <span style="color: blue">using </span>System;
    <span style="color: blue">using </span>System.Data.Entity;
    <span style="color: blue">using </span>System.Data.Entity.Infrastructure;
    
    <span style="color: blue">public partial interface </span><span style="color: #2b91af">IResearchUow
    </span>{
        <span style="color: #2b91af">IDbSet</span>&lt;<span style="color: #2b91af">Car</span>&gt; Car { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
        <span style="color: #2b91af">IDbSet</span>&lt;<span style="color: #2b91af">Person</span>&gt; Person { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
    
        <span style="color: blue">int </span>SaveChanges();
    }
    <span style="color: blue">public partial class </span><span style="color: #2b91af">ResearchUow </span>: <span style="color: #2b91af">DbContext</span>, <span style="color: #2b91af">IResearchUow
    </span>{
        <span style="color: blue">public </span><span style="color: #2b91af">IDbSet</span>&lt;<span style="color: #2b91af">Car</span>&gt; Car { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
        <span style="color: blue">public </span><span style="color: #2b91af">IDbSet</span>&lt;<span style="color: #2b91af">Person</span>&gt; Person { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
    
        <span style="color: blue">public </span>ResearchUow() : <span style="color: blue">base</span>(<span style="color: #a31515">&quot;name=ResearchUow&quot;</span>)
        {
        }
        <span style="color: blue">public </span>ResearchUow(<span style="color: blue">string </span>connection) : <span style="color: blue">base</span>(connection)
        {
        }
        <span style="color: blue">protected override void </span>OnModelCreating(<span style="color: #2b91af">DbModelBuilder </span>modelBuilder)
        {
            <span style="color: blue">throw new </span><span style="color: #2b91af">UnintentionalCodeFirstException</span>();
        }
    }
    <span style="color: blue">public partial class </span><span style="color: #2b91af">MemoryPersistenceResearchUow </span>: <span style="color: #2b91af">ResearchUow
    </span>{
        <span style="color: blue">public </span>MemoryPersistenceResearchUow()
        {
            Seed();
        }
        <span style="color: blue">public void </span>ClearAll()
        {
            <span style="color: blue">this</span>.Car = <span style="color: blue">new </span><span style="color: #2b91af">MemoryPersistenceDbSet</span>&lt;<span style="color: #2b91af">Car</span>&gt;();
            <span style="color: blue">this</span>.Person = <span style="color: blue">new </span><span style="color: #2b91af">MemoryPersistenceDbSet</span>&lt;<span style="color: #2b91af">Person</span>&gt;();
        }
        <span style="color: blue">public override int </span>SaveChanges()
        {
            <span style="color: blue">return </span>0;
        }
    }
}</pre>


<p>&#160;</p>

<p><strong>Add a partial class file for the MemoryPersistenceResearchUow</strong></p>

<p>Every time you update the ReserachModel.edmx from the database or save the T4 templates ResearchModel.tt and ResearchModel.Context.tt, the T4 templates will execute and regenerate all POCO entities and the IResearchUow interface, ResearchUow class and the MemoryPersistenceResearchUow.&#160; To prevent the code that seeds the in-memory UOW to be overwritten a partial class MemoryPersistenceResearchUow is created.</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image20.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image_thumb20.png" width="580" height="402" /></a></p>


<p align="left">
  <pre class="code"><span style="color: blue">public partial class </span><span style="color: #2b91af">MemoryPersistenceResearchUow
</span>{
    <span style="color: blue">public void </span>Seed()
    {
        ClearAll();

        <span style="color: green">// TODO Add seed logic here, like.....
        </span><span style="color: blue">this</span>.Person.Add(<span style="color: blue">new </span><span style="color: #2b91af">Person </span>{ Id = 1, Name = <span style="color: #a31515">&quot;Roel van Lisdonk&quot; </span>});
        <span style="color: blue">this</span>.Car.Add(<span style="color: blue">new </span><span style="color: #2b91af">Car </span>{ Id = 1, NumberPlate = <span style="color: #a31515">&quot;8-KJA-00&quot;</span>, PersonId = 1 });
    }
}</pre>
  Add a IResearchUowFactory and ResearchUowFactory that will contain the logic to create a ResearchUow or an MemoryPersistenceResearchUow.</p>

<pre class="code"><span style="color: blue">namespace </span>Mvc4Application.Models
{
    <span style="color: blue">public interface </span><span style="color: #2b91af">IResearchUowFactory
    </span>{
        <span style="color: #2b91af">IResearchUow </span>GetResearchUow();
    }
}</pre>


<pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Web.Configuration;

<span style="color: blue">namespace </span>Mvc4Application.Models
{
    <span style="color: blue">public class </span><span style="color: #2b91af">ResearchUowFactory </span>: <span style="color: #2b91af">IResearchUowFactory
    </span>{
        <span style="color: blue">public </span><span style="color: #2b91af">IResearchUow </span>GetResearchUow()
        {
            <span style="color: blue">string </span>key = <span style="color: #a31515">&quot;UseStubs&quot;</span>;
            <span style="color: blue">string </span>result = <span style="color: #2b91af">WebConfigurationManager</span>.AppSettings[key];
            <span style="color: blue">if </span>(result == <span style="color: blue">null</span>) { <span style="color: blue">throw new </span><span style="color: #2b91af">ApplicationException</span>(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;Could not find AppSetting[{0}].&quot;</span>, key)); }
            <span style="color: blue">bool </span>useStubs = <span style="color: blue">bool</span>.Parse(result);
            <span style="color: blue">return </span>useStubs ? <span style="color: blue">new </span><span style="color: #2b91af">MemoryPersistenceResearchUow</span>() : <span style="color: blue">new </span><span style="color: #2b91af">ResearchUow</span>();
        }
    }
}</pre>


<p>&#160;</p>

<p>The project will no look like:</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image21.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image_thumb21.png" width="479" height="652" /></a></p>

<p>&#160;</p>

<p><strong>Add appSetting &quot;UseStubs&quot; to the Web.config</strong></p>

<pre class="code">  <span style="color: blue">&lt;</span><span style="color: #a31515">appSettings</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">add </span><span style="color: red">key</span><span style="color: blue">=</span>&quot;<span style="color: blue">UseStubs</span>&quot; <span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">true</span>&quot; <span style="color: blue">/&gt;
</span></pre>


<p>Install an IoC container by using NuGet, in this case I will use ninject:</p>

<p>Install Ninject and Ninject.MVC3 (no MVC4 available yet, but works just fine) this will also install Ninject.Web.Common.</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image22.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image_thumb22.png" width="580" height="388" /></a></p>



<p><strong>In the App_Start folder change the NinjectWebCommon.cs
    <br /></strong>Fill the RegisterService function:</p>

<pre class="code"><span style="color: gray">/// &lt;summary&gt;
/// </span><span style="color: green">Load your modules or register your services here!
</span><span style="color: gray">/// &lt;/summary&gt;
/// &lt;param name=&quot;kernel&quot;&gt;</span><span style="color: green">The kernel.</span><span style="color: gray">&lt;/param&gt;
</span><span style="color: blue">private static void </span>RegisterServices(<span style="color: #2b91af">IKernel </span>kernel)
{
    kernel.Bind&lt;<span style="color: #2b91af">IResearchUowFactory</span>&gt;().To&lt;<span style="color: #2b91af">ResearchUowFactory</span>&gt;();
} </pre>


<p><strong>In the Controllers folder change the HomeControler, add:</strong></p>


<p>
  <pre class="code"><span style="color: blue">private readonly </span><span style="color: #2b91af">IResearchUowFactory </span>_researchUowFactory;
<span style="color: blue">private readonly </span><span style="color: #2b91af">IResearchUow </span>_researchUow;
<span style="color: blue">public </span>HomeController(<span style="color: #2b91af">IResearchUowFactory </span>researchUowFactory)
{
    _researchUowFactory = researchUowFactory;
    _researchUow = _researchUowFactory.GetResearchUow();
}

<span style="color: blue">public </span><span style="color: #2b91af">ActionResult </span>Index()
{
    <span style="color: #2b91af">Person </span>firstPerson = _researchUow.Person.First();
    ViewBag.Message = <span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;First person name [{0}].&quot;</span>, firstPerson.Name);

    <span style="color: blue">return </span>View();
}</pre>
</p>

<p><strong><font size="5">Result</font></strong></p>

<p>This results in:</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image23.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/08/image_thumb23.png" width="580" height="138" /></a></p>

<p>&#160;</p>

<p>The text &quot;First person name [Roel van Lisdonk]&quot; is shown. This was the data from the seed method:</p>

<p><span style="color: blue">this</span>.Person.Add(<span style="color: blue">new </span><span style="color: #2b91af">Person </span>{ Id = 1, Name = <span style="color: #a31515">&quot;Roel van Lisdonk&quot; </span>});</p>

<p>and not from the real database, because the database at this point is empty.</p>

<p>This proves we can switch using in-memory stub data or the real database by changing a appSetting in the web.config.</p>

<p>&#160;</p>

<p>&#160;</p>

<p>&#160;</p>

<p><strong>Don’t forget to fix the unit tests.</strong></p>

<p>In the unit tests for the HomeController, change the lines:</p>

<pre class="code"><span style="color: #2b91af">HomeController </span>controller = <span style="color: blue">new </span><span style="color: #2b91af">HomeController</span>();</pre>

<p>to</p>

<pre class="code"><span style="color: #2b91af">HomeController </span>controller = <span style="color: blue">new </span><span style="color: #2b91af">HomeController</span>(<span style="color: blue">new </span><span style="color: #2b91af">ResearchUowFactory</span>());</pre>


<p>&#160;</p>

<p>&#160;</p>

<p>Now you are able to use the ResearchUow within your HomeController and switch between the MemoryPersistenceResearchUow and the ResearchUow by changing the appSetting UseStubs.</p>
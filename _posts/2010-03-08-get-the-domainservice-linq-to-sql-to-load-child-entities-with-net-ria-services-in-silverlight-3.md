---
ID: 1079
post_title: >
  Get the DomainService (LINQ to SQL) to
  load child entities with .NET RIA
  Services in Silverlight 3
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/08/get-the-domainservice-linq-to-sql-to-load-child-entities-with-net-ria-services-in-silverlight-3/
published: true
post_date: 2010-03-08 20:24:05
---
<p>If you have a table with related tables then you can get the child entries by editing the DomainService and the metadata:   <br />Add the include attribute ([Include()]) to the property containing the child table reference and use the DataLoadOptions to specify the child tables to include in the query result view.</p>  <p>In this case a <strong>Task</strong> table contains a reference to a <strong>Project</strong> table and the Project table contains a reference to the <strong>Customer</strong> table:</p>  <p>&#160;</p>  <p><strong><font size="3">The domainservice class TTSDomainService</font></strong></p>  <pre class="code"><span style="color: green">// TODO: Consider
// 1. Adding parameters to this method and constraining returned results, and/or
// 2. Adding query methods taking different parameters.
</span><span style="color: blue">public </span><span style="color: #2b91af">IQueryable</span>&lt;<span style="color: #2b91af">Task</span>&gt; GetTasks()
{
    <span style="color: green">// Define the child entries to get 
    </span><span style="color: #2b91af">DataLoadOptions </span>options = <span style="color: blue">new </span><span style="color: #2b91af">DataLoadOptions</span>();
    options.LoadWith&lt;<span style="color: #2b91af">Task</span>&gt;(t =&gt; t.Project);
    options.LoadWith&lt;<span style="color: #2b91af">Project</span>&gt;(p =&gt; p.Customer);
    <span style="color: blue">this</span>.DataContext.LoadOptions = options;

    <span style="color: green">// Get the tasks ordered by customer, project, task
    </span><span style="color: blue">return from </span>t <span style="color: blue">in this</span>.DataContext.Tasks
                 <span style="color: blue">orderby </span>t.Project.Customer.Name, t.Project.Name, t.Name
           <span style="color: blue">select </span>t;
}</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p><strong><font size="3">The domainservice meta data class: TTSDomainService.metadata.cs</font></strong></p>

<p>&#160;</p>

<pre class="code"><span style="color: green">// The MetadataTypeAttribute identifies TaskMetadata as the class
// that carries additional metadata for the Task class.
</span>[<span style="color: #2b91af">MetadataTypeAttribute</span>(<span style="color: blue">typeof</span>(<span style="color: #2b91af">Task</span>.<span style="color: #2b91af">TaskMetadata</span>))]
<span style="color: blue">public partial class </span><span style="color: #2b91af">Task
</span>{

    <span style="color: green">// This class allows you to attach custom attributes to properties
    // of the Task class.
    //
    // For example, the following marks the Xyz property as a
    // required field and specifies the format for valid values:
    //    [Required]
    //    [RegularExpression(&quot;[A-Z][A-Za-z0-9]*&quot;)]
    //    [StringLength(32)]
    //    public string Xyz;
    </span><span style="color: blue">internal sealed class </span><span style="color: #2b91af">TaskMetadata
    </span>{

        <span style="color: green">// Metadata classes are not meant to be instantiated.
        </span><span style="color: blue">private </span>TaskMetadata()
        {
        }

        <span style="color: blue">public </span><span style="color: #2b91af">Nullable</span>&lt;<span style="color: blue">int</span>&gt; CategoryAbbrID;

        <span style="color: blue">public int </span>CategoryID;

        <span style="color: blue">public </span><span style="color: #2b91af">Nullable</span>&lt;<span style="color: blue">decimal</span>&gt; EstDuration;

        <span style="color: blue">public </span><span style="color: #2b91af">Nullable</span>&lt;<span style="color: blue">int</span>&gt; HourType;

        <span style="color: blue">public string </span>Name;

   <font size="4">     [<span style="color: #2b91af">Include</span>()]
</font>        <span style="color: blue">public </span><span style="color: #2b91af">Project </span>Project;

        <span style="color: blue">public int </span>ProjectID;

        <span style="color: blue">public </span><span style="color: #2b91af">EntitySet</span>&lt;<span style="color: #2b91af">TaskTimeSpan</span>&gt; TaskTimeSpans;
    }
}</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p>See:</p>

<p><a title="http://chriswalshie.wordpress.com/2009/08/11/masterdetail-binding-with-net-ria-services-and-the-agdatagrid/" href="http://chriswalshie.wordpress.com/2009/08/11/masterdetail-binding-with-net-ria-services-and-the-agdatagrid/">http://chriswalshie.wordpress.com/2009/08/11/masterdetail-binding-with-net-ria-services-and-the-agdatagrid/</a></p>

<p><a href="http://geekswithblogs.net/AzamSharp/archive/2008/03/29/120847.as"></a></p>
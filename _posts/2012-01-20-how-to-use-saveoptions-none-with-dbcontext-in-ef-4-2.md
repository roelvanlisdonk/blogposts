---
ID: 2467
post_title: >
  How to use SaveOptions.None with
  DbContext in EF 4.2
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/01/20/how-to-use-saveoptions-none-with-dbcontext-in-ef-4-2/
published: true
post_date: 2012-01-20 15:29:53
---
<p>If you want to use the SaveOptions.None, when calling the method DbContext.SaveChanges, you must override de function in a partial class, like:</p>  <p>&#160;</p>  <pre class="code"><p><span style="color: gray">/// &lt;summary&gt;
</span><span style="color: gray">/// &lt;/summary&gt;
</span><span style="color: blue">public partial class </span><span style="color: #2b91af">MyEntities </span>: <span style="color: #2b91af">IMyEntities
</span>{
    <span style="color: gray"><font size="1">/// &lt;summary&gt;
    /// </font></span><span style="color: green"><font size="1">Dynamically set connection string and configure Entity Framework.
    </font></span><font size="1"><span style="color: gray">/// &lt;/summary&gt;
    /// &lt;param name=&quot;connection&quot;&gt;&lt;/param&gt;
    </span><span style="color: blue">public </span>Myntities(<span style="color: blue">string </span>connection) : <span style="color: blue">base</span>(connection)
    {
        </font><font size="1"><span style="color: green">// Set Configuration.AutoDetectChangesEnabled = false to improve performance (100x).
        </span>Configuration.AutoDetectChangesEnabled = <span style="color: blue">false</span>;

        </font><font size="1"><span style="color: green">// By default use lazyloading.
        </span>Configuration.LazyLoadingEnabled = <span style="color: blue">true</span>;

        </font><font size="1"><span style="color: green">// Don't valid entities on save.
        </span>Configuration.ValidateOnSaveEnabled = <span style="color: blue">false</span>;
    }</font></p><p>
    <span style="color: gray"><strong>/// &lt;summary&gt;
    /// </strong></span><span style="color: green"><strong>Override the default save changes so, because we have disabled &quot;AutoDetectChangesEnabled&quot;. 
    </strong></span><strong><span style="color: gray">/// &lt;/summary&gt;
    /// &lt;returns&gt;&lt;/returns&gt;
    </span><span style="color: blue">public override int </span>SaveChanges()
    {
        <span style="color: blue">return </span>(<span style="color: blue">this as </span><span style="color: #2b91af">IObjectContextAdapter</span>).ObjectContext.SaveChanges(System.Data.Objects.<span style="color: #2b91af">SaveOptions</span>.None);
    }</strong></p><p><strong></strong>&#160;</p><p><strong></strong>
}
</p></pre>
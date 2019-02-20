---
ID: 1584
post_title: >
  Showing a many to many relationship in a
  GridView by using Entity Framework 4.0,
  EntityDataSource and data binding in ASP
  .NET 4.0
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/07/02/showing-a-many-to-many-relationship-in-a-gridview-by-using-entity-framework-4-0-entitydatasource-and-data-binding-in-asp-net-4-0/
published: true
post_date: 2010-07-02 13:07:14
---
<p>The Microsoft SQL Server 2008 R2 sample database AdventureWorks, contains a table Product which as a many to many relationship with the table Document, via the junction table ProductDocument. This post describes the steps you will have to take to show all products and per product all document titles.</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/07/image.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/07/image_thumb.png" width="754" height="576" /></a> </p>  <p>&#160;</p>  <p>As you can see, product “506” has a relationship with multiple documents, so the column “Documents” shows 2 titles.&#160; Because there can be more then one document title to show, I use a BulletedList, but you also could use a&#160; CheckBoxList or DropDownList.</p>  <p>&#160;</p>  <p><strong>The data model</strong></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/07/image1.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/07/image_thumb1.png" width="454" height="598" /></a> </p>  <p>&#160;</p>  <p><strong>ASP .NET (*.aspx) page</strong></p> <a href="http://11011.net/software/vspaste"></a><a href="http://11011.net/software/vspaste"></a>  <pre class="code"><span style="background: yellow">&lt;%</span><span style="color: blue">@ </span><span style="color: maroon">Page </span><span style="color: red">Title</span><span style="color: blue">=&quot;&quot; </span><span style="color: red">Language</span><span style="color: blue">=&quot;C#&quot; </span><span style="color: red">MasterPageFile</span><span style="color: blue">=&quot;~/Site.Master&quot; </span><span style="color: red">AutoEventWireup</span><span style="color: blue">=&quot;true&quot; 
</span><span style="color: red">CodeBehind</span><span style="color: blue">=&quot;ManyToManyGridView.aspx.cs&quot; 
</span><span style="color: red">Inherits</span><span style="color: blue">=&quot;Rvl.Demo.AspNet4.EF.WebApplication.Pages.ManyToManyGridView&quot; </span><span style="background: yellow">%&gt;
</span><span style="color: blue">&lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">Content </span><span style="color: red">ID</span><span style="color: blue">=&quot;Content1&quot; </span><span style="color: red">ContentPlaceHolderID</span><span style="color: blue">=&quot;HeadContent&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;</span><span style="color: maroon">link </span><span style="color: red">href</span><span style="color: blue">=&quot;../Styles/ManyToManyGridView.css&quot; </span><span style="color: red">rel</span><span style="color: blue">=&quot;stylesheet&quot; </span><span style="color: red">type</span><span style="color: blue">=&quot;text/css&quot; /&gt;
&lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">Content</span><span style="color: blue">&gt;
&lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">Content </span><span style="color: red">ID</span><span style="color: blue">=&quot;Content2&quot; </span><span style="color: red">ContentPlaceHolderID</span><span style="color: blue">=&quot;MainContent&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;</span><span style="color: maroon">p </span><span style="color: red">class</span><span style="color: blue">=&quot;pageTitle&quot;&gt;</span>Products<span style="color: blue">&lt;/</span><span style="color: maroon">p</span><span style="color: blue">&gt;
    &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">GridView </span><span style="color: red">ID</span><span style="color: blue">=&quot;GridView1&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">AllowPaging</span><span style="color: blue">=&quot;true&quot; </span><span style="color: red">DataKeyNames</span><span style="color: blue">=&quot;ProductID&quot; 
         </span><span style="color: red">AutoGenerateColumns</span><span style="color: blue">=&quot;false&quot; </span><span style="color: red">PageSize</span><span style="color: blue">=&quot;50&quot; </span><span style="color: red">DataSourceID</span><span style="color: blue">=&quot;GridViewEntityDataSource&quot;&gt;
        &lt;</span><span style="color: maroon">Columns</span><span style="color: blue">&gt;
            &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">BoundField </span><span style="color: red">DataField</span><span style="color: blue">=&quot;ProductID&quot; </span><span style="color: red">HeaderText</span><span style="color: blue">=&quot;Id&quot; </span><span style="color: red">ItemStyle-CssClass</span><span style="color: blue">=&quot;columnPadding&quot; 
            </span><span style="color: red">HeaderStyle-CssClass</span><span style="color: blue">=&quot;columnPadding&quot; /&gt;
            &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">BoundField </span><span style="color: red">DataField</span><span style="color: blue">=&quot;Name&quot; </span><span style="color: red">HeaderText</span><span style="color: blue">=&quot;Name&quot; </span><span style="color: red">ItemStyle-CssClass</span><span style="color: blue">=&quot;columnPadding&quot; 
            </span><span style="color: red">HeaderStyle-CssClass</span><span style="color: blue">=&quot;columnPadding&quot; /&gt;
            &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">TemplateField</span><span style="color: blue">&gt;
                &lt;</span><span style="color: maroon">HeaderTemplate</span><span style="color: blue">&gt;
                    &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">Label </span><span style="color: red">ID</span><span style="color: blue">=&quot;documentsHeaderLabel&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">Text</span><span style="color: blue">=&quot;Documents&quot;&gt;&lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">Label</span><span style="color: blue">&gt;
                &lt;/</span><span style="color: maroon">HeaderTemplate</span><span style="color: blue">&gt;
                &lt;</span><span style="color: maroon">HeaderStyle </span><span style="color: red">CssClass</span><span style="color: blue">=&quot;columnPadding&quot; /&gt;
                &lt;</span><span style="color: maroon">ItemStyle </span><span style="color: red">CssClass</span><span style="color: blue">=&quot;columnPadding&quot; /&gt;
                &lt;</span><span style="color: maroon">ItemTemplate</span><span style="color: blue">&gt;
                    &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">BulletedList </span><span style="color: red">DataSource</span><span style="color: blue">='</span><span style="background: yellow">&lt;%</span><span style="color: blue"># </span>FillBulletedList(Container) <span style="background: yellow">%&gt;</span><span style="color: blue">' 
                    </span><span style="color: red">ID</span><span style="color: blue">=&quot;documentsBulletedList&quot; </span><span style="color: red">DataValueField</span><span style="color: blue">=&quot;DocumentID&quot; </span><span style="color: red">DataTextField</span><span style="color: blue">=&quot;Title&quot; 
                    </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;&lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">BulletedList</span><span style="color: blue">&gt;
                 &lt;/</span><span style="color: maroon">ItemTemplate</span><span style="color: blue">&gt;
            &lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">TemplateField</span><span style="color: blue">&gt;
        &lt;/</span><span style="color: maroon">Columns</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">GridView</span><span style="color: blue">&gt;
    </span><span style="color: #006400">&lt;!--
       - Set EnableFlattening to &quot;false&quot;, so you can use real &quot;Product&quot; entities in the FillBulletedList 
         function and not wrapper (System.Web.UI.WebControls.EntityDataSourceWrapper) classes, generated 
         by the entity framework.
       - Don't use the &quot;Include&quot; property, this property should load related entities, like 
         &quot;ProductDocument&quot; and &quot;Document&quot;, but in my case in did not work, use the &quot;OnQueryCreated&quot; event
         to provide a complicated inner join query, that loads related entities
    --&gt;
    </span><span style="color: blue">&lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">EntityDataSource </span><span style="color: red">ID</span><span style="color: blue">=&quot;GridViewEntityDataSource&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">EnableDelete</span><span style="color: blue">=&quot;false&quot; 
        </span><span style="color: red">EnableInsert</span><span style="color: blue">=&quot;false&quot; </span><span style="color: red">EnableUpdate</span><span style="color: blue">=&quot;false&quot; 
        </span><span style="color: red">ContextTypeName</span><span style="color: blue">=&quot;Rvl.Demo.AspNet4.EF.WebApplication.Dal.AdventureWorksEntities&quot; 
        </span><span style="color: red">ConnectionString</span><span style="color: blue">=&quot;name=AdventureWorksEntities&quot; </span><span style="color: red">DefaultContainerName</span><span style="color: blue">=&quot;AdventureWorksEntities&quot; 
        </span><span style="color: red">EntitySetName</span><span style="color: blue">=&quot;Product&quot; </span><span style="color: red">EnableFlattening</span><span style="color: blue">=&quot;false&quot; 
        </span><span style="color: red">OnQueryCreated</span><span style="color: blue">=&quot;GridViewEntityDataSource_QueryCreated&quot;&gt;
    &lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">EntityDataSource</span><span style="color: blue">&gt;
&lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">Content</span><span style="color: blue">&gt;

</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p><strong>ASP .NET (*.cs) code behind page</strong></p>

<pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Web;
<span style="color: blue">using </span>System.Web.UI;
<span style="color: blue">using </span>System.Web.UI.WebControls;
<span style="color: blue">using </span>Rvl.Demo.AspNet4.EF.WebApplication.Dal;
<span style="color: blue">using </span>System.Data.Objects;

<span style="color: blue">namespace </span>Rvl.Demo.AspNet4.EF.WebApplication.Pages
{
    <span style="color: blue">public partial class </span><span style="color: #2b91af">ManyToManyGridView </span>: System.Web.UI.<span style="color: #2b91af">Page
    </span>{
        <span style="color: blue">protected void </span>Page_Load(<span style="color: blue">object </span>sender, <span style="color: #2b91af">EventArgs </span>e)
        {   
        }
        <span style="color: blue">public </span><span style="color: #2b91af">List</span>&lt;<span style="color: #2b91af">Document</span>&gt; FillBulletedList(<span style="color: blue">object </span>container)
        {
            <span style="color: green">// Get the product from the current row
            </span><span style="color: #2b91af">GridViewRow </span>gvr = container <span style="color: blue">as </span><span style="color: #2b91af">GridViewRow</span>;
            <span style="color: #2b91af">Product </span>product = gvr.DataItem <span style="color: blue">as </span><span style="color: #2b91af">Product</span>;

            <span style="color: green">// Create a list of documents related to the current product
            </span><span style="color: #2b91af">List</span>&lt;<span style="color: #2b91af">Document</span>&gt; documents = <span style="color: blue">new </span><span style="color: #2b91af">List</span>&lt;<span style="color: #2b91af">Document</span>&gt;();
            <span style="color: blue">foreach </span>(<span style="color: #2b91af">ProductDocument </span>pd <span style="color: blue">in </span>product.ProductDocument)
            {
                documents.Add(pd.Document);
            }

            <span style="color: blue">return </span>documents;
        }
        <span style="color: blue">protected void </span>GridViewEntityDataSource_QueryCreated(<span style="color: blue">object </span>sender, <span style="color: #2b91af">QueryCreatedEventArgs </span>e)
        {
            <span style="color: green">// Load related entities (&quot;ProductDocument&quot; and &quot;Document&quot;)
            </span><span style="color: #2b91af">ObjectQuery</span>&lt;<span style="color: #2b91af">Product</span>&gt; query = e.Query.Cast&lt;<span style="color: #2b91af">Product</span>&gt;() <span style="color: blue">as </span><span style="color: #2b91af">ObjectQuery</span>&lt;<span style="color: #2b91af">Product</span>&gt;;
            <span style="color: #2b91af">AdventureWorksEntities </span>context = query.Context <span style="color: blue">as </span><span style="color: #2b91af">AdventureWorksEntities</span>;
            context.Product.Include(<span style="color: #a31515">&quot;ProductDocument&quot;</span>).Include(<span style="color: #a31515">&quot;Document&quot;</span>);

            <span style="color: green">// Show only product with related documents, by using a inner join (from .... from)
            // Show only unique rows by using &quot;Distinct&quot;
            // Show products ordered by name, by using &quot;orderby&quot;
            </span><span style="color: blue">var </span>items = <span style="color: blue">from </span>ps <span style="color: blue">in
                            </span>((<span style="color: blue">from </span>p <span style="color: blue">in </span>query
                              <span style="color: blue">from </span>pd <span style="color: blue">in </span>p.ProductDocument
                              <span style="color: blue">select </span>p).Distinct())
                        <span style="color: blue">orderby </span>ps.Name
                        <span style="color: blue">select </span>ps;
            e.Query = items;
        }
    }
}</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>The EntityDataSource use the OnQueryCreated event to provide an inner join query, that loads related entities, like “ProductDocument” and “Document”. It does not use the “Include” property, because that did not work in my case, I don’t no why, but I don’t have time to investigate. The “Include” is done on the Context of the query.</p>

<p>The GridView uses a TemplateField column and the '&lt;%# … %&gt;' syntax to call a function for every row in the GridView to fill a BulletedList that shows all documents per product.</p>
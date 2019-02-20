---
ID: 1514
post_title: >
  Using the ASP .NET 4.0 DetailsView
  ItemCommand event to set the value of a
  fields textbox (edit modus) or label
  (read modus)
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/06/21/using-the-asp-net-4-0-detailsview-itemcommand-event-to-set-the-value-of-a-fields-textbox-edit-modus-or-label-read-modus/
published: true
post_date: 2010-06-21 14:35:00
---
<p align="left">If you are using ASP .NET DetailsView control and use a TemplateField containing a textbox for displaying the fields text and a LinkButton to update the textbox on postback, you should use the DetailsView.ItemCommand event and the DetailsView.FindControl method to set the text of the textbox or label, depending on the DetailsView.DefaultMode.</p>  <p align="left">It uses the ADO .NET Entitiy Framework 4.0, declarative binding and the Microsoft SQL Server 2008 R2 RTM sample database AdventureWorks. The page is the “detail” part of a Master – Detail view, so you must supply the ProductCategory to show in the request querystring, like <a title="http://localhost:52109/ProductCategoryDetails.aspx?Id=4" href="http://localhost:52109/ProductCategoryDetails.aspx?Id=4">http://localhost:52109/ProductCategoryDetails.aspx?Id=4</a></p>  <p align="left">   <br />    <br /><strong>Code</strong></p>  <pre class="code"><span style="color: blue">protected void </span>PageDetailsView_ItemCommand(<span style="color: blue">object </span>sender, <span style="color: #2b91af">DetailsViewCommandEventArgs </span>e)
        {
            <span style="color: blue">if </span>(<span style="color: blue">this</span>.PageDetailsView.DefaultMode == <span style="color: #2b91af">DetailsViewMode</span>.ReadOnly)
            {
                <span style="color: blue">if </span>(e.CommandName.Equals(<span style="color: #a31515">&quot;GenerateModifiedDate&quot;</span>, <span style="color: #2b91af">StringComparison</span>.CurrentCultureIgnoreCase))
                {
                    <span style="color: #2b91af">Label </span>modifiedDateLabel = <span style="color: blue">this</span>.PageDetailsView.FindControl(<span style="color: #a31515">&quot;ModifiedDateLabel&quot;</span>) <span style="color: blue">as </span><span style="color: #2b91af">Label</span>;
                    modifiedDateLabel.Text = <span style="color: #2b91af">DateTime</span>.Now.ToString();
                }
            }
            <span style="color: blue">else
            </span>{
                <span style="color: blue">if </span>(e.CommandName.Equals(<span style="color: #a31515">&quot;GenerateModifiedDate&quot;</span>, <span style="color: #2b91af">StringComparison</span>.CurrentCultureIgnoreCase))
                {
                    <span style="color: #2b91af">TextBox </span>modifiedDateTextbox = <span style="color: blue">this</span>.PageDetailsView.FindControl(<span style="color: #a31515">&quot;ModifiedDateTextbox&quot;</span>) <span style="color: blue">as </span><span style="color: #2b91af">TextBox</span>;
                    modifiedDateTextbox.Text = <span style="color: #2b91af">DateTime</span>.Now.ToString();
                }
            }
        }</pre>

<p>&#160;</p>

<p><strong>Screendump</strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/06/image12.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/06/image_thumb12.png" width="754" height="551" /></a> </p>

<p>By clicking on the Generate LinkButton in the DetailsView the ModifiedDate will be updated.</p>

<p>&#160;</p>

<p><strong>ProductCategoryDetails.aspx</strong></p>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<pre class="code"><span style="background: yellow">&lt;%</span><span style="color: blue">@ </span><span style="color: maroon">Page </span><span style="color: red">MasterPageFile</span><span style="color: blue">=&quot;~/Site.master&quot; </span><span style="color: red">Language</span><span style="color: blue">=&quot;C#&quot; </span><span style="color: red">AutoEventWireup</span><span style="color: blue">=&quot;true&quot; </span><span style="color: red">CodeBehind</span><span style="color: blue">=&quot;ProductCategoryDetails.aspx.cs&quot; </span><span style="color: red">Inherits</span><span style="color: blue">=&quot;Demo.WebApplication.ProductCategoryDetails&quot; </span><span style="background: yellow">%&gt;

</span><span style="color: blue">&lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">Content </span><span style="color: red">ID</span><span style="color: blue">=&quot;HeaderContent&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">ContentPlaceHolderID</span><span style="color: blue">=&quot;HeadContent&quot;&gt;
    &lt;</span><span style="color: maroon">link </span><span style="color: red">href</span><span style="color: blue">=&quot;Styles/ProductCategoryDetails.css&quot; </span><span style="color: red">rel</span><span style="color: blue">=&quot;stylesheet&quot; </span><span style="color: red">type</span><span style="color: blue">=&quot;text/css&quot; /&gt;
&lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">Content</span><span style="color: blue">&gt;
&lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">Content </span><span style="color: red">ID</span><span style="color: blue">=&quot;PageContent&quot; </span><span style="color: red">ContentPlaceHolderID</span><span style="color: blue">=&quot;MainContent&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">DetailsView 
        </span><span style="color: red">ID</span><span style="color: blue">=&quot;PageDetailsView&quot; 
        </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;
        </span><span style="color: red">DataSourceID</span><span style="color: blue">=&quot;PageDataSource&quot;
        </span><span style="color: red">AllowPaging</span><span style="color: blue">=&quot;false&quot;
        </span><span style="color: red">AutoGenerateDeleteButton</span><span style="color: blue">=&quot;true&quot;
        </span><span style="color: red">AutoGenerateEditButton</span><span style="color: blue">=&quot;true&quot;
        </span><span style="color: red">AutoGenerateInsertButton</span><span style="color: blue">=&quot;true&quot;
        </span><span style="color: red">AutoGenerateRows</span><span style="color: blue">=&quot;false&quot;
        </span><span style="color: red">EmptyDataText</span><span style="color: blue">=&quot;No record found!&quot;
        </span><span style="color: red">DefaultMode</span><span style="color: blue">=&quot;Edit&quot;
        </span><span style="color: red">DataKeyNames</span><span style="color: blue">=&quot;ProductCategoryID&quot; 
        </span><span style="color: red">onitemcommand</span><span style="color: blue">=&quot;PageDetailsView_ItemCommand&quot;&gt;
        &lt;</span><span style="color: maroon">Fields</span><span style="color: blue">&gt;
            &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">BoundField
                </span><span style="color: red">DataField</span><span style="color: blue">=&quot;ProductCategoryID&quot;
                </span><span style="color: red">HeaderText</span><span style="color: blue">=&quot;ProductCategoryID&quot;&gt;
            &lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">BoundField</span><span style="color: blue">&gt;
            &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">BoundField
                </span><span style="color: red">DataField</span><span style="color: blue">=&quot;Name&quot;
                </span><span style="color: red">HeaderText</span><span style="color: blue">=&quot;Name&quot;&gt;
            &lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">BoundField</span><span style="color: blue">&gt;
            &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">BoundField
                </span><span style="color: red">DataField</span><span style="color: blue">=&quot;rowguid&quot;
                </span><span style="color: red">HeaderText</span><span style="color: blue">=&quot;rowguid&quot;&gt;
            &lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">BoundField</span><span style="color: blue">&gt;
            &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">TemplateField</span><span style="color: blue">&gt;
                &lt;</span><span style="color: maroon">HeaderTemplate</span><span style="color: blue">&gt;
                    &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">Label </span><span style="color: red">ID</span><span style="color: blue">=&quot;ModifiedDateHeaderLabel&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">Text</span><span style="color: blue">=&quot;ModifiedDate&quot;&gt;&lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">Label</span><span style="color: blue">&gt;
                &lt;/</span><span style="color: maroon">HeaderTemplate</span><span style="color: blue">&gt;
                    &lt;</span><span style="color: maroon">ItemTemplate</span><span style="color: blue">&gt;
                    &lt;</span><span style="color: maroon">div</span><span style="color: blue">&gt;
                    &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">Label </span><span style="color: red">ID</span><span style="color: blue">=&quot;ModifiedDateLabel&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">Text</span><span style="color: blue">='</span><span style="background: yellow">&lt;%</span><span style="color: blue"># </span>Bind(&quot;ModifiedDate&quot;) <span style="background: yellow">%&gt;</span><span style="color: blue">'&gt;&lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">Label</span><span style="color: blue">&gt;
                    &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LinkButton </span><span style="color: red">ID</span><span style="color: blue">=&quot;ModifiedDateLinkButton&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">CssClass</span><span style="color: blue">=&quot;generateLinkButton&quot; </span><span style="color: red">CommandName</span><span style="color: blue">=&quot;GenerateModifiedDate&quot;&gt;</span>Generate<span style="color: blue">&lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LinkButton</span><span style="color: blue">&gt;
                    &lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
                &lt;/</span><span style="color: maroon">ItemTemplate</span><span style="color: blue">&gt;
                &lt;</span><span style="color: maroon">EditItemTemplate</span><span style="color: blue">&gt;
                    &lt;</span><span style="color: maroon">div</span><span style="color: blue">&gt;
                    &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">TextBox </span><span style="color: red">ID</span><span style="color: blue">=&quot;ModifiedDateTextBox&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">Text</span><span style="color: blue">='</span><span style="background: yellow">&lt;%</span><span style="color: blue"># </span>Bind(&quot;ModifiedDate&quot;) <span style="background: yellow">%&gt;</span><span style="color: blue">'&gt;&lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">TextBox</span><span style="color: blue">&gt;
                    &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LinkButton </span><span style="color: red">ID</span><span style="color: blue">=&quot;ModifiedDateLinkButton&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">CssClass</span><span style="color: blue">=&quot;generateLinkButton&quot; </span><span style="color: red">CommandName</span><span style="color: blue">=&quot;GenerateModifiedDate&quot;&gt;</span>Generate<span style="color: blue">&lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LinkButton</span><span style="color: blue">&gt;
                    &lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
                &lt;/</span><span style="color: maroon">EditItemTemplate</span><span style="color: blue">&gt;
            &lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">TemplateField</span><span style="color: blue">&gt;
        &lt;/</span><span style="color: maroon">Fields</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">DetailsView</span><span style="color: blue">&gt;
    &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">EntityDataSource 
        </span><span style="color: red">ID</span><span style="color: blue">=&quot;PageDataSource&quot; 
        </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; 
        </span><span style="color: red">EnableDelete</span><span style="color: blue">=&quot;true&quot; 
        </span><span style="color: red">EnableInsert</span><span style="color: blue">=&quot;true&quot; 
        </span><span style="color: red">EnableUpdate</span><span style="color: blue">=&quot;true&quot;
        </span><span style="color: red">ConnectionString</span><span style="color: blue">=&quot;name=AdventureWorksEntities&quot;
        </span><span style="color: red">DefaultContainerName</span><span style="color: blue">=&quot;AdventureWorksEntities&quot;
        </span><span style="color: red">EntitySetName</span><span style="color: blue">=&quot;ProductCategory&quot;
        </span><span style="color: red">Where</span><span style="color: blue">=&quot;it.[ProductCategoryID]=@ProductCategoryID&quot;&gt;
        &lt;</span><span style="color: maroon">WhereParameters</span><span style="color: blue">&gt; 
            &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">QueryStringParameter </span><span style="color: red">DbType</span><span style="color: blue">=&quot;Int32&quot; </span><span style="color: red">Name</span><span style="color: blue">=&quot;ProductCategoryID&quot; </span><span style="color: red">QueryStringField</span><span style="color: blue">=&quot;Id&quot; /&gt; 
        &lt;/</span><span style="color: maroon">WhereParameters</span><span style="color: blue">&gt; 
    &lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">EntityDataSource</span><span style="color: blue">&gt;
&lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">Content</span><span style="color: blue">&gt;



</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p>This is part of a very simple ASP .NET demo web application I created, see <a title="http://www.roelvanlisdonk.nl/?p=1521" href="http://www.roelvanlisdonk.nl/?p=1521">http://www.roelvanlisdonk.nl/?p=1521</a></p>
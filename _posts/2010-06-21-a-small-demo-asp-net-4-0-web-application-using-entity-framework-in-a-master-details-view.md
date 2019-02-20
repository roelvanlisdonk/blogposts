---
ID: 1521
post_title: 'A small demo ASP .NET 4.0 Web Application, using Entity Framework in a Master &ndash; Details view'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/06/21/a-small-demo-asp-net-4-0-web-application-using-entity-framework-in-a-master-details-view/
published: true
post_date: 2010-06-21 14:54:50
---
<p>I just created a small demo ASP .NET 4.0 Web Application, it uses:</p>  <p>- ASP .NET 4.0 </p>  <p>- Ajax</p>  <p>- Declarative DataBinding using a EntityDataSource </p>  <p>- DetailsView (master – details view, by using a RadGrid and a DetailsView) </p>  <p>- Entity Framework 4.0 </p>  <p>- Masterpage and contentpages </p>  <p>- Microsoft SQL Server 2008 R2 RTM sample database AdventureWorks</p>  <p>- Stylesheet for the master page and per contentpage 1 styelsheet </p>  <p>- Telerik RadGrid</p>  <p>&#160;</p>  <p><strong>Screendump Master View (ProductCategoryOverview)</strong></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/06/image10.png"><img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/06/image_thumb10.png" width="754" height="551" /></a> </p>  <p>When you click on the “Edit” link a new page will be shown (ProductCategoryDetails.aspx)</p>  <p>&#160;</p>  <p><strong>Screendump Detials View (ProductCategoryDetails.aspx)</strong></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/06/image11.png"><img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/06/image_thumb11.png" width="754" height="551" /></a> </p>  <p>&#160;</p>  <p><strong>Site.master</strong></p>  <pre class="code"><span style="background: yellow">&lt;%</span><span style="color: blue">@ </span><span style="color: maroon">Master </span><span style="color: red">Language</span><span style="color: blue">=&quot;C#&quot; </span><span style="color: red">AutoEventWireup</span><span style="color: blue">=&quot;true&quot; </span><span style="color: red">CodeBehind</span><span style="color: blue">=&quot;Site.master.cs&quot; </span><span style="color: red">Inherits</span><span style="color: blue">=&quot;Demo.WebApplication.Site&quot; </span><span style="background: yellow">%&gt;
&lt;%</span><span style="color: blue">@ </span><span style="color: maroon">Register </span><span style="color: red">Assembly</span><span style="color: blue">=&quot;Telerik.Web.UI&quot; </span><span style="color: red">Namespace</span><span style="color: blue">=&quot;Telerik.Web.UI&quot; </span><span style="color: red">TagPrefix</span><span style="color: blue">=&quot;telerik&quot; </span><span style="background: yellow">%&gt;

</span><span style="color: blue">&lt;!</span><span style="color: maroon">DOCTYPE </span><span style="color: red">html PUBLIC </span><span style="color: blue">&quot;-//W3C//DTD XHTML 1.0 Transitional//EN&quot; &quot;http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd&quot;&gt;

&lt;</span><span style="color: maroon">html </span><span style="color: red">xmlns</span><span style="color: blue">=&quot;http://www.w3.org/1999/xhtml&quot;&gt;
&lt;</span><span style="color: maroon">head </span><span style="color: red">id</span><span style="color: blue">=&quot;Head1&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;</span><span style="color: maroon">title</span><span style="color: blue">&gt;</span>PowerPivot Demo WebApplication<span style="color: blue">&lt;/</span><span style="color: maroon">title</span><span style="color: blue">&gt;
    &lt;</span><span style="color: maroon">link </span><span style="color: red">href</span><span style="color: blue">=&quot;Styles/Master.css&quot; </span><span style="color: red">rel</span><span style="color: blue">=&quot;stylesheet&quot; </span><span style="color: red">type</span><span style="color: blue">=&quot;text/css&quot; /&gt;
    &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">ContentPlaceHolder </span><span style="color: red">ID</span><span style="color: blue">=&quot;HeadContent&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">ContentPlaceHolder</span><span style="color: blue">&gt;
&lt;/</span><span style="color: maroon">head</span><span style="color: blue">&gt;
&lt;</span><span style="color: maroon">body</span><span style="color: blue">&gt;
&lt;</span><span style="color: maroon">form </span><span style="color: red">id</span><span style="color: blue">=&quot;Form1&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">class</span><span style="color: blue">=&quot;form&quot;&gt;
&lt;</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">RadScriptManager </span><span style="color: red">ID</span><span style="color: blue">=&quot;generalRadScriptManager&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; /&gt;
</span><span style="color: #006400">&lt;!-- One RadAjaxManager for all content pages --&gt; 
</span><span style="color: blue">&lt;</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">RadAjaxManager </span><span style="color: red">ID</span><span style="color: blue">=&quot;generalRadAjaxManager&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; /&gt;
</span><span style="color: #006400">&lt;!-- One RadAjaxLoadingPanel for all content pages --&gt; 
</span><span style="color: blue">&lt;</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">RadAjaxLoadingPanel </span><span style="color: red">ID</span><span style="color: blue">=&quot;generalRadAjaxLoadingPanel&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">BackgroundPosition</span><span style="color: blue">=&quot;Center&quot; </span><span style="color: red">Skin</span><span style="color: blue">=&quot;Default&quot; /&gt;
&lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;page&quot;&gt;
    &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;inside&quot;&gt;
        &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;header&quot;&gt;
            &lt;</span><span style="color: maroon">img </span><span style="color: red">alt</span><span style="color: blue">=&quot;PowerPivot Logo&quot; </span><span style="color: red">src</span><span style="color: blue">=&quot;Images/PowerPivot_Logo.png&quot;/&gt;
            </span><span style="color: #006400">&lt;!-- All postback's in the RadAjaxPanel1 will be converted to AJAX postback's and the page will not flicker on navigation --&gt;
            </span><span style="color: blue">&lt;</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">RadAjaxPanel </span><span style="color: red">ID</span><span style="color: blue">=&quot;RadAjaxPanel1&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">LoadingPanelID</span><span style="color: blue">=&quot;generalRadAjaxLoadingPanel&quot;&gt;
                &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;navigation&quot;&gt;
                    &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;navigationPrimary&quot;&gt;
                        &lt;</span><span style="color: maroon">ul</span><span style="color: blue">&gt; 
                            &lt;</span><span style="color: maroon">li</span><span style="color: blue">&gt;&lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LinkButton </span><span style="color: red">ID</span><span style="color: blue">=&quot;administrationLinkButton&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">onclick</span><span style="color: blue">=&quot;AdministrationLinkButton_Click&quot;&gt;</span>Manage<span style="color: blue">&lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LinkButton</span><span style="color: blue">&gt;&lt;/</span><span style="color: maroon">li</span><span style="color: blue">&gt;
                            &lt;</span><span style="color: maroon">li</span><span style="color: blue">&gt;&lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LinkButton </span><span style="color: red">ID</span><span style="color: blue">=&quot;zakelijkLinkButton&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">onclick</span><span style="color: blue">=&quot;AdministrationLinkButton_Click&quot;&gt;</span>View<span style="color: blue">&lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LinkButton</span><span style="color: blue">&gt;&lt;/</span><span style="color: maroon">li</span><span style="color: blue">&gt;
                        &lt;/</span><span style="color: maroon">ul</span><span style="color: blue">&gt;
                    &lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
                    &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;navigationSeparator&quot;&gt;&lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
                    &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;navigationSecondairy&quot;&gt;
                        &lt;</span><span style="color: maroon">ul</span><span style="color: blue">&gt; 
                            &lt;</span><span style="color: maroon">li</span><span style="color: blue">&gt;&lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LinkButton </span><span style="color: red">ID</span><span style="color: blue">=&quot;customerLinkButton&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">onclick</span><span style="color: blue">=&quot;CustomerLinkButton_Click&quot;&gt;</span>Customer<span style="color: blue">&lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LinkButton</span><span style="color: blue">&gt;&lt;/</span><span style="color: maroon">li</span><span style="color: blue">&gt;
                            &lt;</span><span style="color: maroon">li</span><span style="color: blue">&gt;&lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LinkButton </span><span style="color: red">ID</span><span style="color: blue">=&quot;ProductLinkButton&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">onclick</span><span style="color: blue">=&quot;ProductLinkButton_Click&quot;&gt;</span>Product<span style="color: blue">&lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">LinkButton</span><span style="color: blue">&gt;&lt;/</span><span style="color: maroon">li</span><span style="color: blue">&gt;
                            &lt;</span><span style="color: maroon">li</span><span style="color: blue">&gt;&lt;/</span><span style="color: maroon">li</span><span style="color: blue">&gt;
                        &lt;/</span><span style="color: maroon">ul</span><span style="color: blue">&gt;
                    &lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
                &lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
            &lt;/</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">RadAjaxPanel</span><span style="color: blue">&gt;
        &lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
        &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;content&quot;&gt;
            &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">ContentPlaceHolder </span><span style="color: red">ID</span><span style="color: blue">=&quot;MainContent&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; /&gt;
        &lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
        &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;footerPlaceholder&quot;&gt;&lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
    &lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">=&quot;footer&quot;&gt;
        &lt;</span><span style="color: maroon">ul </span><span style="color: red">class</span><span style="color: blue">=&quot;footerLeftNav&quot;&gt;
        &lt;</span><span style="color: maroon">li</span><span style="color: blue">&gt;</span>Contact Us<span style="color: blue">&lt;/</span><span style="color: maroon">li</span><span style="color: blue">&gt;
        &lt;</span><span style="color: maroon">li</span><span style="color: blue">&gt;</span>Privacy Statement<span style="color: blue">&lt;/</span><span style="color: maroon">li</span><span style="color: blue">&gt;
        &lt;/</span><span style="color: maroon">ul</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
&lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
&lt;/</span><span style="color: maroon">form</span><span style="color: blue">&gt;
&lt;/</span><span style="color: maroon">body</span><span style="color: blue">&gt;
&lt;/</span><span style="color: maroon">html</span><span style="color: blue">&gt;


</span></pre>

<p>&#160;</p>

<p><strong>ProductCategoryOverview.aspx</strong></p>

<pre class="code"><span style="background: yellow">&lt;%</span><span style="color: blue">@ </span><span style="color: maroon">Page </span><span style="color: red">MasterPageFile</span><span style="color: blue">=&quot;~/Site.master&quot;  </span><span style="color: red">Language</span><span style="color: blue">=&quot;C#&quot; </span><span style="color: red">AutoEventWireup</span><span style="color: blue">=&quot;true&quot; </span><span style="color: red">CodeBehind</span><span style="color: blue">=&quot;ProductCategoryOverview.aspx.cs&quot; </span><span style="color: red">Inherits</span><span style="color: blue">=&quot;Demo.WebApplication.ProductCategoryOverview&quot; </span><span style="background: yellow">%&gt;
&lt;%</span><span style="color: blue">@ </span><span style="color: maroon">Register </span><span style="color: red">Assembly</span><span style="color: blue">=&quot;Telerik.Web.UI&quot; </span><span style="color: red">Namespace</span><span style="color: blue">=&quot;Telerik.Web.UI&quot; </span><span style="color: red">TagPrefix</span><span style="color: blue">=&quot;telerik&quot; </span><span style="background: yellow">%&gt;

</span><span style="color: blue">&lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">Content </span><span style="color: red">ID</span><span style="color: blue">=&quot;HeaderContent&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">ContentPlaceHolderID</span><span style="color: blue">=&quot;HeadContent&quot;&gt;
    &lt;</span><span style="color: maroon">link </span><span style="color: red">href</span><span style="color: blue">=&quot;Styles/ProductCategoryOverview.css&quot; </span><span style="color: red">rel</span><span style="color: blue">=&quot;stylesheet&quot; </span><span style="color: red">type</span><span style="color: blue">=&quot;text/css&quot; /&gt;
&lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">Content</span><span style="color: blue">&gt;
&lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">Content </span><span style="color: red">ID</span><span style="color: blue">=&quot;PageContent&quot; </span><span style="color: red">ContentPlaceHolderID</span><span style="color: blue">=&quot;MainContent&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">RadGrid 
        </span><span style="color: red">ID</span><span style="color: blue">=&quot;PageRadGrid&quot;
        </span><span style="color: red">AllowFilteringByColumn</span><span style="color: blue">=&quot;True&quot;
        </span><span style="color: red">AllowPaging</span><span style="color: blue">=&quot;True&quot;
        </span><span style="color: red">AllowSorting</span><span style="color: blue">=&quot;True&quot;
        </span><span style="color: red">AutoGenerateColumns</span><span style="color: blue">=&quot;False&quot;
        </span><span style="color: red">ShowStatusBar</span><span style="color: blue">=&quot;True&quot;
        </span><span style="color: red">DataSourceID</span><span style="color: blue">=&quot;PageDataSource&quot;
        </span><span style="color: red">EnableLinqExpressions</span><span style="color: blue">=&quot;false&quot;
        </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;
        </span><span style="color: red">PageSize</span><span style="color: blue">=&quot;25&quot;&gt;
        &lt;</span><span style="color: maroon">PagerStyle </span><span style="color: red">Mode</span><span style="color: blue">=&quot;NextPrevAndNumeric&quot;&gt;&lt;/</span><span style="color: maroon">PagerStyle</span><span style="color: blue">&gt;
        &lt;</span><span style="color: maroon">MasterTableView </span><span style="color: red">CommandItemDisplay</span><span style="color: blue">=&quot;Top&quot;&gt;
            &lt;</span><span style="color: maroon">NoRecordsTemplate</span><span style="color: blue">&gt;
                &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">Label </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">ID</span><span style="color: blue">=&quot;noItemsLabel&quot; </span><span style="color: red">Text</span><span style="color: blue">=&quot;No records found!&quot;&gt;&lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">Label</span><span style="color: blue">&gt;
            &lt;/</span><span style="color: maroon">NoRecordsTemplate</span><span style="color: blue">&gt;
            &lt;</span><span style="color: maroon">CommandItemTemplate</span><span style="color: blue">&gt;
                &lt;</span><span style="color: maroon">a </span><span style="color: red">class</span><span style="color: blue">=&quot;addLink&quot; </span><span style="color: red">href</span><span style="color: blue">=&quot;ProductCategoryDetails.aspx?Id=-1&quot;&gt;</span>Add new record<span style="color: blue">&lt;/</span><span style="color: maroon">a</span><span style="color: blue">&gt;
                &lt;</span><span style="color: maroon">a </span><span style="color: red">class</span><span style="color: blue">=&quot;refreshLink&quot; </span><span style="color: red">href</span><span style="color: blue">=&quot;ProductCategoryOverview.aspx&quot;&gt;</span>Refresh<span style="color: blue">&lt;/</span><span style="color: maroon">a</span><span style="color: blue">&gt;
            &lt;/</span><span style="color: maroon">CommandItemTemplate</span><span style="color: blue">&gt;
            &lt;</span><span style="color: maroon">SortExpressions</span><span style="color: blue">&gt;
               &lt;</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">GridSortExpression </span><span style="color: red">FieldName</span><span style="color: blue">=&quot;Name&quot; </span><span style="color: red">SortOrder</span><span style="color: blue">=&quot;Ascending&quot; /&gt;
            &lt;/</span><span style="color: maroon">SortExpressions</span><span style="color: blue">&gt;
            &lt;</span><span style="color: maroon">Columns</span><span style="color: blue">&gt;
                &lt;</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">GridHyperlinkColumn
                    </span><span style="color: red">AllowFiltering</span><span style="color: blue">=&quot;false&quot;
                    </span><span style="color: red">UniqueName</span><span style="color: blue">=&quot;EditColumn&quot;
                    </span><span style="color: red">DataTextFormatString</span><span style="color: blue">=&quot;Edit&quot;
                    </span><span style="color: red">DataTextField</span><span style="color: blue">=&quot;ProductCategoryID&quot;
                    </span><span style="color: red">DataNavigateUrlFields</span><span style="color: blue">=&quot;ProductCategoryID&quot;
                    </span><span style="color: red">DataNavigateUrlFormatString</span><span style="color: blue">=&quot;~/ProductCategoryDetails.aspx?Id={0}&quot;
                    </span><span style="color: red">meta</span><span style="color: blue">:</span><span style="color: red">resourcekey</span><span style="color: blue">=&quot;EditColumn&quot;&gt;
                &lt;/</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">GridHyperlinkColumn</span><span style="color: blue">&gt;
                &lt;</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">GridButtonColumn 
                    </span><span style="color: red">CommandName</span><span style="color: blue">=&quot;Delete&quot; 
                    </span><span style="color: red">meta</span><span style="color: blue">:</span><span style="color: red">resourcekey</span><span style="color: blue">=&quot;DeleteColumn&quot;
                    </span><span style="color: red">UniqueName</span><span style="color: blue">=&quot;DeleteColumn&quot;  
                    </span><span style="color: red">ConfirmText</span><span style="color: blue">=&quot;Delete this customer?&quot; 
                    </span><span style="color: red">Text</span><span style="color: blue">=&quot;Delete&quot;&gt;
                &lt;/</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">GridButtonColumn</span><span style="color: blue">&gt;
                &lt;</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">GridBoundColumn 
                    </span><span style="color: red">AutoPostBackOnFilter</span><span style="color: blue">=&quot;true&quot;
                    </span><span style="color: red">CurrentFilterFunction</span><span style="color: blue">=&quot;EqualTo&quot;
                    </span><span style="color: red">DataField</span><span style="color: blue">=&quot;ProductCategoryID&quot;
                    </span><span style="color: red">FilterControlWidth</span><span style="color: blue">=&quot;100px&quot;
                    </span><span style="color: red">HeaderText</span><span style="color: blue">=&quot;Id&quot;
                    </span><span style="color: red">meta</span><span style="color: blue">:</span><span style="color: red">resourcekey</span><span style="color: blue">=&quot;ProductCategoryIDColumn&quot; 
                    </span><span style="color: red">UniqueName</span><span style="color: blue">=&quot;ProductCategoryID&quot; 
                    </span><span style="color: red">SortExpression</span><span style="color: blue">=&quot;ProductCategoryID&quot;  
                    </span><span style="color: red">ShowFilterIcon</span><span style="color: blue">=&quot;true&quot;&gt;
                    &lt;</span><span style="color: maroon">ItemStyle </span><span style="color: red">Width</span><span style="color: blue">=&quot;100px&quot; /&gt;
                &lt;/</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">GridBoundColumn</span><span style="color: blue">&gt;
                &lt;</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">GridBoundColumn 
                    </span><span style="color: red">AutoPostBackOnFilter</span><span style="color: blue">=&quot;true&quot;
                    </span><span style="color: red">CurrentFilterFunction</span><span style="color: blue">=&quot;Contains&quot;
                    </span><span style="color: red">DataField</span><span style="color: blue">=&quot;Name&quot;
                    </span><span style="color: red">FilterControlWidth</span><span style="color: blue">=&quot;100px&quot;
                    </span><span style="color: red">HeaderText</span><span style="color: blue">=&quot;Name&quot;
                    </span><span style="color: red">meta</span><span style="color: blue">:</span><span style="color: red">resourcekey</span><span style="color: blue">=&quot;NameColumn&quot; 
                    </span><span style="color: red">UniqueName</span><span style="color: blue">=&quot;Name&quot; 
                    </span><span style="color: red">SortExpression</span><span style="color: blue">=&quot;Name&quot;  
                    </span><span style="color: red">ShowFilterIcon</span><span style="color: blue">=&quot;true&quot;&gt;
                    &lt;</span><span style="color: maroon">ItemStyle </span><span style="color: red">Width</span><span style="color: blue">=&quot;100px&quot; /&gt;
                &lt;/</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">GridBoundColumn</span><span style="color: blue">&gt;
                &lt;</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">GridBoundColumn 
                    </span><span style="color: red">AutoPostBackOnFilter</span><span style="color: blue">=&quot;true&quot;
                    </span><span style="color: red">CurrentFilterFunction</span><span style="color: blue">=&quot;Contains&quot;
                    </span><span style="color: red">DataField</span><span style="color: blue">=&quot;rowguid&quot;
                    </span><span style="color: red">FilterControlWidth</span><span style="color: blue">=&quot;200px&quot;
                    </span><span style="color: red">HeaderText</span><span style="color: blue">=&quot;rowguid&quot;
                    </span><span style="color: red">meta</span><span style="color: blue">:</span><span style="color: red">resourcekey</span><span style="color: blue">=&quot;rowguidColumn&quot; 
                    </span><span style="color: red">UniqueName</span><span style="color: blue">=&quot;rowguid&quot; 
                    </span><span style="color: red">SortExpression</span><span style="color: blue">=&quot;rowguid&quot;  
                    </span><span style="color: red">ShowFilterIcon</span><span style="color: blue">=&quot;true&quot;&gt;
                    &lt;</span><span style="color: maroon">ItemStyle </span><span style="color: red">Width</span><span style="color: blue">=&quot;200px&quot; /&gt;
                &lt;/</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">GridBoundColumn</span><span style="color: blue">&gt;
                &lt;</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">GridBoundColumn 
                    </span><span style="color: red">AutoPostBackOnFilter</span><span style="color: blue">=&quot;true&quot;
                    </span><span style="color: red">CurrentFilterFunction</span><span style="color: blue">=&quot;Contains&quot;
                    </span><span style="color: red">DataField</span><span style="color: blue">=&quot;ModifiedDate&quot;
                    </span><span style="color: red">FilterControlWidth</span><span style="color: blue">=&quot;200px&quot;
                    </span><span style="color: red">HeaderText</span><span style="color: blue">=&quot;ModifiedDate&quot;
                    </span><span style="color: red">meta</span><span style="color: blue">:</span><span style="color: red">resourcekey</span><span style="color: blue">=&quot;ModifiedDateColumn&quot; 
                    </span><span style="color: red">UniqueName</span><span style="color: blue">=&quot;ModifiedDate&quot; 
                    </span><span style="color: red">SortExpression</span><span style="color: blue">=&quot;ModifiedDate&quot;  
                    </span><span style="color: red">ShowFilterIcon</span><span style="color: blue">=&quot;true&quot;&gt;
                    &lt;</span><span style="color: maroon">ItemStyle </span><span style="color: red">Width</span><span style="color: blue">=&quot;200px&quot; /&gt;
                &lt;/</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">GridBoundColumn</span><span style="color: blue">&gt;
            &lt;/</span><span style="color: maroon">Columns</span><span style="color: blue">&gt;
        &lt;/</span><span style="color: maroon">MasterTableView</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">RadGrid</span><span style="color: blue">&gt;
    
    &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">EntityDataSource 
        </span><span style="color: red">ID</span><span style="color: blue">=&quot;PageDataSource&quot; 
        </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; 
        </span><span style="color: red">EnableDelete</span><span style="color: blue">=&quot;true&quot; 
        </span><span style="color: red">EnableInsert</span><span style="color: blue">=&quot;true&quot; 
        </span><span style="color: red">EnableUpdate</span><span style="color: blue">=&quot;true&quot;
        </span><span style="color: red">ConnectionString</span><span style="color: blue">=&quot;name=AdventureWorksEntities&quot;
        </span><span style="color: red">DefaultContainerName</span><span style="color: blue">=&quot;AdventureWorksEntities&quot;
        </span><span style="color: red">EntitySetName</span><span style="color: blue">=&quot;ProductCategory&quot;
        &gt;
    &lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">EntityDataSource</span><span style="color: blue">&gt;
&lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">Content</span><span style="color: blue">&gt;

</span></pre>

<p><a href="http://11011.net/software/vspaste"></a></p>

<p><strong>ProductCategoryDetails.aspx</strong></p>

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

<p><strong>Note:</strong> In my application I must use “it” before the column name in the Where property of the EntityDataSource, else I will get an exception: </p>

<p><font color="#800000" size="1">System.Web.HttpUnhandledException (0x80004005): Exception of type 'System.Web.HttpUnhandledException' was thrown. ---&gt; System.Data.EntitySqlException: 'ProductCategoryID' could not be resolved in the current scope or context. Make sure that all referenced variables are in scope, that required schemas are loaded, and that namespaces are referenced correctly. Near escaped identifier, line 6, column 1. at System.Web.UI.WebControls.EntityDataSourceView.ExecuteSelect(DataSourceSelectArguments arguments) at System.Web.UI.DataSourceView.Select(DataSourceSelectArguments arguments, DataSourceViewSelectCallback callback) at System.Web.UI.WebControls.DataBoundControl.PerformSelect() at System.Web.UI.WebControls.BaseDataBoundControl.DataBind() at System.Web.UI.WebControls.DetailsView.DataBind() at System.Web.UI.WebControls.BaseDataBoundControl.EnsureDataBound() at System.Web.UI.WebControls.DetailsView.EnsureDataBound() at System.Web.UI.WebControls.CompositeDataBoundControl.CreateChildControls() at System.Web.UI.Control.EnsureChildControls() at System.Web.UI.Control.PreRenderRecursiveInternal() at System.Web.UI.Control.PreRenderRecursiveInternal() at System.Web.UI.Control.PreRenderRecursiveInternal() at System.Web.UI.Control.PreRenderRecursiveInternal() at System.Web.UI.Control.PreRenderRecursiveInternal() at System.Web.UI.Page.ProcessRequestMain(Boolean includeStagesBeforeAsyncPoint, Boolean includeStagesAfterAsyncPoint) at System.Web.UI.Page.HandleError(Exception e) at System.Web.UI.Page.ProcessRequestMain(Boolean includeStagesBeforeAsyncPoint, Boolean includeStagesAfterAsyncPoint) at System.Web.UI.Page.ProcessRequest(Boolean includeStagesBeforeAsyncPoint, Boolean includeStagesAfterAsyncPoint) at System.Web.UI.Page.ProcessRequest() at System.Web.UI.Page.ProcessRequestWithNoAssert(HttpContext context) at System.Web.UI.Page.ProcessRequest(HttpContext context) at ASP.productcategorydetails_aspx.ProcessRequest(HttpContext context) in c:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\f1d0d8b4\9eb9cfbd\App_Web_2z53k4nc.5.cs:line 0 at System.Web.HttpApplication.CallHandlerExecutionStep.System.Web.HttpApplication.IExecutionStep.Execute() at System.Web.HttpApplication.ExecuteStep(IExecutionStep step, Boolean&amp; completedSynchronously</font></p>

<p>&#160;</p>

<p><strong>ProductCategoryDetails.aspx.cs</strong></p>

<pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Web;
<span style="color: blue">using </span>System.Web.UI;
<span style="color: blue">using </span>System.Web.UI.WebControls;

<span style="color: blue">namespace </span>Demo.WebApplication
{
    <span style="color: blue">public partial class </span><span style="color: #2b91af">ProductCategoryDetails </span>: System.Web.UI.<span style="color: #2b91af">Page
    </span>{
        <span style="color: blue">protected void </span>Page_Load(<span style="color: blue">object </span>sender, <span style="color: #2b91af">EventArgs </span>e)
        {

        }

        <span style="color: blue">protected void </span>PageDetailsView_ItemCommand(<span style="color: blue">object </span>sender, <span style="color: #2b91af">DetailsViewCommandEventArgs </span>e)
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
        }
    }
}</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p><strong>Master.css</strong></p>

<pre class="code"><span style="color: maroon">*
</span>{
    <span style="color: red">margin</span>: <span style="color: blue">0px</span>; <span style="color: #006400">/* All elements start with 0px margin */
    </span><span style="color: red">padding</span>: <span style="color: blue">0px</span>;  <span style="color: #006400">/* All elements start with 0px padding */
</span>}
<span style="color: maroon">html
</span>{
    <span style="color: red">height</span>: <span style="color: blue">100%</span>; <span style="color: #006400">/* Must be 100% for footer at the bottom of the page */
    </span><span style="color: red">font-family</span>: <span style="color: blue">Arial, Helvetica, sans-serif</span>;
    <span style="color: red">font-size</span>: <span style="color: blue">100%</span>;
    <span style="color: red">font-weight</span>: <span style="color: blue">normal</span>;
    <span style="color: red">color</span>: <span style="color: blue">#222</span>;
}
<span style="color: maroon">body
</span>{
    <span style="color: red">height</span>: <span style="color: blue">100%</span>; <span style="color: #006400">/* Must be 100% for footer at the bottom of the page */
</span>}
<span style="color: maroon">form
</span>{
    <span style="color: red">height</span>: <span style="color: blue">100%</span>; <span style="color: #006400">/* Must be 100% for footer at the bottom of the page */
</span>}
<span style="color: maroon">a
</span>{
    <span style="color: red">color</span>: <span style="color: blue">#222</span>;
    <span style="color: red">text-decoration</span>: <span style="color: blue">none</span>;
}
<span style="color: maroon">a:hover
</span>{
    <span style="color: red">color</span>: <span style="color: blue">#222</span>;
    <span style="color: red">text-decoration</span>: <span style="color: blue">underline</span>;
}
<span style="color: maroon">div.page
</span>{
    <span style="color: red">margin-right</span>: <span style="color: blue">auto</span>; <span style="color: #006400">/* Center the page */
    </span><span style="color: red">margin-left</span>:<span style="color: blue">auto</span>; <span style="color: #006400">/* Center the page */
    </span><span style="color: red">height</span>: <span style="color: blue">100%</span>;  <span style="color: #006400">/* Must be 100% for footer at the bottom of the page */
    </span><span style="color: red">text-align</span>: <span style="color: blue">left</span>;
    <span style="color: red">width</span>: <span style="color: blue">1000px</span>; <span style="color: #006400">/* Fixed width for screen resolution 1024px optimalisation */
</span>}
<span style="color: maroon">div.inside
</span>{
    <span style="color: red">border-left</span>: <span style="color: blue">1px solid rgb(224,225,226)</span>;
    <span style="color: red">border-right</span>: <span style="color: blue">1px solid rgb(224,225,226)</span>;
    <span style="color: red">min-height</span>: <span style="color: blue">100%</span>;  <span style="color: #006400">/* Must be 100% for footer at the bottom of the page, using min-height instead of height allows content to be larger then intial page size */
    </span><span style="color: red">margin-bottom</span>: <span style="color: blue">-33px</span>; <span style="color: #006400">/* Negative bottom margin is used for correct the 100% height with the height of the footer, else vertical scrollbars will be shown */
</span>}
<span style="color: maroon">div.header
</span>{
    <span style="color: red">padding</span>: <span style="color: blue">10px 0px 8px 0px</span>;
}
<span style="color: maroon">div.header img
</span>{
    <span style="color: red">height</span>: <span style="color: blue">60px</span>;
    <span style="color: red">margin-left</span>: <span style="color: blue">20px</span>;
}
<span style="color: maroon">div.content
</span>{
    <span style="color: red">color</span>: <span style="color: blue">#666</span>;
    <span style="color: red">font-size</span>: <span style="color: blue">70%</span>;
    <span style="color: red">padding</span>: <span style="color: blue">20px 15px 15px 15px</span>;
}
<span style="color: maroon">div.navigation
</span>{
    <span style="color: red">border-bottom</span>: <span style="color: blue">2px solid rgb(143,208,64)</span>;
    <span style="color: red">position</span>: <span style="color: blue">absolute</span>;
    <span style="color: red">top</span>: <span style="color: blue">0px</span>;
    <span style="color: red">width</span>: <span style="color: blue">998px</span>;
}
<span style="color: maroon">div.navigationSeparator
</span>{
    <span style="color: red">border-top</span>: <span style="color: blue">1px solid rgb(222,222,222)</span>;
    <span style="color: red">margin-left</span>: <span style="color: blue">279px</span>;
}
<span style="color: maroon">div.navigationPrimary ul
</span>{
    <span style="color: red">height</span>: <span style="color: blue">26px</span>;
    <span style="color: red">margin-top</span>: <span style="color: blue">13px</span>;
    <span style="color: red">padding-left</span>: <span style="color: blue">299px</span>;
}
<span style="color: maroon">div.navigationPrimary ul li
</span>{
    <span style="color: red">background</span>: <span style="color: blue">url(../Images/TabLeft.gif) no-repeat scroll left top</span>;
    <span style="color: red">float</span>: <span style="color: blue">left</span>; <span style="color: #006400">/* Makes the unoderdered list flow horizontal instead of vertical */
    </span><span style="color: red">font-weight</span>: <span style="color: blue">bold</span>;
    <span style="color: red">font-size</span>: <span style="color: blue">75%</span>;
    <span style="color: red">height</span>: <span style="color: blue">26px</span>;
    <span style="color: red">line-height</span>: <span style="color: blue">26px</span>;
    <span style="color: red">list-style-type</span>: <span style="color: blue">none</span>; <span style="color: #006400">/* Don't display bullets */
    </span><span style="color: red">margin</span>: <span style="color: blue">0px 4px 0px 0px</span>;
    <span style="color: red">text-decoration</span>: <span style="color: blue">none</span>;
    <span style="color: red">text-transform</span>: <span style="color: blue">uppercase</span>;
    <span style="color: red">white-space</span>: <span style="color: blue">nowrap</span>;
}
<span style="color: maroon">div.navigationPrimary ul li a
</span>{
    <span style="color: red">background</span>: <span style="color: blue">url(../Images/TabRight.gif) no-repeat scroll right top</span>;
    <span style="color: red">float</span>: <span style="color: blue">left</span>;
    <span style="color: red">height</span>: <span style="color: blue">26px</span>;
    <span style="color: red">line-height</span>: <span style="color: blue">26px</span>;
    <span style="color: red">padding</span>: <span style="color: blue">0px 15px 0px 15px</span>;
}
<span style="color: maroon">div.navigationPrimary ul li a:hover
</span>{
    <span style="color: red">color</span>: <span style="color: blue">rgb(143,208,64)</span>;
}
<span style="color: maroon">div.navigationSecondairy ul
</span>{
    <span style="color: red">padding-left</span>: <span style="color: blue">310px</span>;
    <span style="color: red">margin-top</span>: 
}
<span style="color: maroon">div.navigationSecondairy ul li
</span>{
    <span style="color: red">border-left</span>: <span style="color: blue">1px solid rgb(143,208,64)</span>;
    <span style="color: red">float</span>: <span style="color: blue">left</span>; <span style="color: #006400">/* Makes the unoderdered list flow horizontal instead of vertical */
    </span><span style="color: red">font-size</span>: <span style="color: blue">80%</span>;
    <span style="color: red">list-style-type</span>: <span style="color: blue">none</span>; <span style="color: #006400">/* Don't display bullets */
    </span><span style="color: red">margin</span>: <span style="color: blue">10px 12px 10px 0px</span>;
    <span style="color: red">padding-left</span>: <span style="color: blue">10px</span>;
    <span style="color: red">white-space</span>: <span style="color: blue">nowrap</span>;
}
<span style="color: maroon">div.navigationSecondairy ul li a
</span>{
    <span style="color: red">float</span>: <span style="color: blue">left</span>;
}
<span style="color: maroon">div.navigationSecondairy ul li a:hover
</span>{
    <span style="color: red">color</span>: <span style="color: blue">rgb(143,208,64)</span>;
}
<span style="color: maroon">div.footerPlaceholder
</span>{
    <span style="color: red">height</span>: <span style="color: blue">33px</span>; <span style="color: #006400">/* The height should be equal to the full height of the footer (including any padding or borders you may add). Without the &quot;footerPlaceholder&quot; div, the content will flow beneath the footer */
</span>}
<span style="color: maroon">div.footer
</span>{
    <span style="color: red">background-color</span>: <span style="color: blue">rgb(143,208,64)</span>;
    <span style="color: red">color</span>: <span style="color: blue">rgb(255,255,255)</span>;
    <span style="color: red">font-size</span>: <span style="color: blue">60%</span>;
    <span style="color: red">padding</span>: <span style="color: blue">10px 46px 10px 46px</span>;
    <span style="color: red">width</span>: <span style="color: blue">906px</span>;
}
<span style="color: maroon">ul.footerLeftNav
</span>{
    <span style="color: red">margin</span>: <span style="color: blue">0px</span>;
    <span style="color: red">padding</span>: <span style="color: blue">0px</span>;
    <span style="color: red">page-break-inside</span>: <span style="color: blue">avoid</span>;
    <span style="color: red">list-style-position</span>: <span style="color: blue">outside</span>;
    <span style="color: red">list-style-type</span>: <span style="color: blue">none</span>;
}
<span style="color: maroon">ul.footerLeftNav li
</span>{
    <span style="color: red">display</span>: <span style="color: blue">inline</span>;
    <span style="color: red">padding-right</span>: <span style="color: blue">18px</span>;
}</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p><strong>ProductCategoryOverview.css</strong></p>

<pre class="code"><span style="color: maroon">div.content
</span>{
    <span style="color: red">padding-top</span>: <span style="color: blue">30px</span>;
}
<span style="color: maroon">div.content a:hover
</span>{
    <span style="color: red">text-decoration</span>: <span style="color: blue">underline</span>;
}
<span style="color: maroon">a.addLink
</span>{
    <span style="color: red">background</span>: <span style="color: blue">url(../Images/AddCross.gif) no-repeat scroll left center</span>;
    <span style="color: red">cursor</span>: <span style="color: blue">pointer</span>;
    <span style="color: red">float</span>: <span style="color: blue">left</span>;
    <span style="color: red">margin</span>: <span style="color: blue">5px 0px 5px 10px</span>;
    <span style="color: red">padding-left</span>: <span style="color: blue">20px</span>;
}
<span style="color: maroon">a.refreshLink
</span>{
    <span style="color: red">background</span>: <span style="color: blue">url(../Images/Refresh.gif) no-repeat scroll right center</span>;
    <span style="color: red">cursor</span>: <span style="color: blue">pointer</span>;
    <span style="color: red">float</span>: <span style="color: blue">right</span>;
    <span style="color: red">margin</span>: <span style="color: blue">5px 10px 5px 0px</span>;
    <span style="color: red">padding-right</span>: <span style="color: blue">22px</span>;
}</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p><strong>ProductCategoryDetails.css</strong></p>

<pre class="code"><span style="color: maroon">div.content a.generateLinkButton
</span>{
    <span style="color: red">margin-left</span>: <span style="color: blue">25px</span>;
    <span style="color: red">color</span>: <span style="color: blue">Blue</span>;
}
<span style="color: maroon">div.content table
</span>{
    <span style="color: red">border</span>: <span style="color: blue">none</span>;
}
<span style="color: maroon">div.content td
</span>{
    <span style="color: red">border</span>: <span style="color: blue">none</span>;
    <span style="color: red">padding</span>: <span style="color: blue">2px 5px 2px 5px</span>;
    <span style="color: red">white-space</span>: <span style="color: blue">nowrap</span>;
}
<span style="color: maroon">div.content input[type=text]
</span>{
    <span style="color: red">width</span>: <span style="color: blue">300px</span>;
}</pre>
<a href="http://11011.net/software/vspaste"></a>
---
ID: 1557
post_title: >
  Showing, Styling and DataBind items in
  an ASP .NET 4.0 CheckBoxList using CSS
  and EF4.0
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/06/24/showing-and-styling-items-in-a-checkboxlist-using-css-and-ef4-0/
published: true
post_date: 2010-06-24 11:01:02
---
<p>I wanted to show records in the ProductCategory table of the SQL Server AdventureWorks database in a ASP .NET 4.0 by using a CheckBoxList, without writing any code.</p>  <p><strong></strong></p>  <p><strong>Result</strong></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/06/image20.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/06/image_thumb20.png" width="754" height="485" /></a> </p>  <p>&#160;</p>  <p><strong>CheckedListBox.aspx</strong></p>  <pre class="code"><span style="background: yellow">&lt;%</span><span style="color: blue">@ </span><span style="color: maroon">Page </span><span style="color: red">Language</span><span style="color: blue">=&quot;C#&quot; </span><span style="color: red">MasterPageFile</span><span style="color: blue">=&quot;~/Site.master&quot; </span><span style="color: red">AutoEventWireup</span><span style="color: blue">=&quot;true&quot; </span><span style="color: red">CodeBehind</span><span style="color: blue">=&quot;CheckedListBox.aspx.cs&quot; </span><span style="color: red">Inherits</span><span style="color: blue">=&quot;Rvl.Demo.AspNet4.EF.WebApplication.Pages.CheckedListBox&quot; </span><span style="background: yellow">%&gt;

</span><span style="color: blue">&lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">Content </span><span style="color: red">ID</span><span style="color: blue">=&quot;HeaderContent&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">ContentPlaceHolderID</span><span style="color: blue">=&quot;HeadContent&quot;&gt;
    &lt;</span><span style="color: maroon">link </span><span style="color: red">href</span><span style="color: blue">=&quot;../Styles/CheckedListBox.css&quot; </span><span style="color: red">rel</span><span style="color: blue">=&quot;stylesheet&quot; </span><span style="color: red">type</span><span style="color: blue">=&quot;text/css&quot; /&gt;
&lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">Content</span><span style="color: blue">&gt;
&lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">Content </span><span style="color: red">ID</span><span style="color: blue">=&quot;BodyContent&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">ContentPlaceHolderID</span><span style="color: blue">=&quot;MainContent&quot;&gt;
    &lt;</span><span style="color: maroon">h2</span><span style="color: blue">&gt;
        </span>CheckedListBox page
    <span style="color: blue">&lt;/</span><span style="color: maroon">h2</span><span style="color: blue">&gt;
    &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">CheckBoxList 
        </span><span style="color: red">ID</span><span style="color: blue">=&quot;PcCheckBoxList&quot; 
        </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;
        </span><span style="color: red">DataSourceID</span><span style="color: blue">=&quot;PcDataSource&quot;
        </span><span style="color: red">DataTextField</span><span style="color: blue">=&quot;Name&quot;
        </span><span style="color: red">DataValueField</span><span style="color: blue">=&quot;ProductCategoryID&quot;<br />        <font color="#ff0000">ondatabound</font>=&quot;PcCheckBoxList_DataBound&quot;&gt;
    &lt;/</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">CheckBoxList</span><span style="color: blue">&gt;
    &lt;</span><span style="color: maroon">asp</span><span style="color: blue">:</span><span style="color: maroon">EntityDataSource 
        </span><span style="color: red">ID</span><span style="color: blue">=&quot;PcDataSource&quot; 
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
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p><strong>CheckedListBox.css</strong></p>

<pre class="code"><span style="color: maroon">div.main h2
</span>{
    <span style="color: red">margin-bottom</span>: <span style="color: blue">10px</span>;
}
<span style="color: maroon">div.main label
</span>{
    <span style="color: red">padding-left</span>: <span style="color: blue">30px</span>;
}</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>You can style the labels of the checkboxes with&#160; CSS, because they are rendered as &lt;input type=”checkbox” … /&gt;&lt;label for=”…”&gt;&lt;/label&gt; in html, like:</p>

<p>&#160;</p>

<p><font size="1">&lt;table id=&quot;MainContent_PcCheckBoxList&quot;&gt;</font></p>

<p><font size="1">&lt;tr&gt;</font></p>

<p><font size="1">&lt;td&gt;&lt;input id=&quot;MainContent_PcCheckBoxList_0&quot; type=&quot;checkbox&quot; name=&quot;ctl00$MainContent$PcCheckBoxList$0&quot; value=&quot;1&quot; /&gt;&lt;label for=&quot;MainContent_PcCheckBoxList_0&quot;&gt;Bikes&lt;/label&gt;&lt;/td&gt;</font></p>

<p><font size="1">&lt;/tr&gt;&lt;tr&gt;</font></p>

<p><font size="1">&lt;td&gt;&lt;input id=&quot;MainContent_PcCheckBoxList_1&quot; type=&quot;checkbox&quot; name=&quot;ctl00$MainContent$PcCheckBoxList$1&quot; value=&quot;2&quot; /&gt;&lt;label for=&quot;MainContent_PcCheckBoxList_1&quot;&gt;Components&lt;/label&gt;&lt;/td&gt;</font></p>

<p><font size="1">&lt;/tr&gt;&lt;tr&gt;</font></p>

<p><font size="1">&lt;td&gt;&lt;input id=&quot;MainContent_PcCheckBoxList_2&quot; type=&quot;checkbox&quot; name=&quot;ctl00$MainContent$PcCheckBoxList$2&quot; value=&quot;3&quot; /&gt;&lt;label for=&quot;MainContent_PcCheckBoxList_2&quot;&gt;Clothing&lt;/label&gt;&lt;/td&gt;</font></p>

<p><font size="1">&lt;/tr&gt;&lt;tr&gt;</font></p>

<p><font size="1">&lt;td&gt;&lt;input id=&quot;MainContent_PcCheckBoxList_3&quot; type=&quot;checkbox&quot; name=&quot;ctl00$MainContent$PcCheckBoxList$3&quot; value=&quot;4&quot; /&gt;&lt;label for=&quot;MainContent_PcCheckBoxList_3&quot;&gt;Accessories&lt;/label&gt;&lt;/td&gt;</font></p>

<p><font size="1">&lt;/tr&gt;</font></p>

<p><font size="1">&lt;/table&gt;</font></p>

<p>&#160;</p>

<p><strong>DataBind to Selected property</strong></p>

<p>You can’t declaratively bind to the “Selected” property of you CheckBoxList items.</p>

<p>So if you want to check some checkboxes in the CheckBoxList, you should do that in the <strong>DataBound</strong> event of the CheckBoxList control. This event will fire after the control is databound, so it is filled with items.</p>

<pre class="code"><span style="color: blue">protected void </span>PcCheckBoxList_DataBound(<span style="color: blue">object </span>sender, <span style="color: #2b91af">EventArgs </span>e)
        {
            <span style="color: green">// Check the first and last item
            </span><span style="color: blue">this</span>.PcCheckBoxList.Items[0].Selected = <span style="color: blue">true</span>;
            <span style="color: blue">this</span>.PcCheckBoxList.Items[3].Selected = <span style="color: blue">true</span>;

            <span style="color: green">// To check them all, use:
            //foreach (ListItem li in this.PcCheckBoxList.Items)
            //{
            //    li.Selected = true;
            //}
        </span>}</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p>&#160;</p>

<p><strong>Solution Explorer (Project Structure)</strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/06/image17.png"><img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/06/image_thumb17.png" width="404" height="582" /></a> </p>

<p>&#160;</p>

<p><strong>Steps</strong></p>

<ol>
  <li>Create a new ASP .NET 4.0 WebApplication in VS2010 </li>

  <li>Add a ADO .NET Entity Data Model (connected to the SQL Server 2008 R2 AdventureWorks database) </li>

  <li>Add the ProductCategory table to you’re ADO .NET Entity Data Model </li>

  <li>Add a Web Form (CheckedListBox.aspx) </li>

  <li>Add a Style Sheet (CheckedListBox.css) </li>

  <li>Set CheckedListBox.aspx as startup page </li>

  <li>Run the project </li>
</ol>
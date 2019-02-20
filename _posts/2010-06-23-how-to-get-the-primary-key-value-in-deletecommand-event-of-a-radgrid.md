---
ID: 1541
post_title: >
  How to get the primary key value in
  DeleteCommand event of a RadGrid
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/06/23/how-to-get-the-primary-key-value-in-deletecommand-event-of-a-radgrid/
published: true
post_date: 2010-06-23 10:46:38
---
<p>First of all you should set the MasterTableView.DataKeyNames property of the RadGrid to the primary key columns:   <br />&lt;MasterTableView DataKeyNames=&quot;Id&quot;&gt;</p>  <pre class="code"><p> <span style="color: blue">&lt;</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">RadGrid 
        </span><span style="color: red">ID</span><span style="color: blue">=&quot;customerOverviewRadGrid&quot;
        </span><span style="color: red">AllowFilteringByColumn</span><span style="color: blue">=&quot;True&quot;
        </span><span style="color: red">AllowPaging</span><span style="color: blue">=&quot;True&quot;
        </span><span style="color: red">AllowSorting</span><span style="color: blue">=&quot;True&quot;
        </span><span style="color: red">AutoGenerateColumns</span><span style="color: blue">=&quot;False&quot;
        </span><span style="color: red">DataSourceID</span><span style="color: blue">=&quot;customersDS&quot;
        </span><span style="color: red">EnableLinqExpressions</span><span style="color: blue">=&quot;false&quot;
        </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;
        </span><span style="color: red">ondeletecommand</span><span style="color: blue">=&quot;customerOverviewRadGrid_DeleteCommand&quot; 
</span><span style="color: blue">        &gt;
        &lt;</span><span style="color: maroon">PagerStyle </span><span style="color: red">Mode</span><span style="color: blue">=&quot;NextPrevAndNumeric&quot;&gt;&lt;/</span><span style="color: maroon">PagerStyle</span><span style="color: blue">&gt;
        &lt;</span><span style="color: maroon">MasterTableView </span><span style="color: red">DataKeyNames</span><span style="color: blue">=&quot;Id&quot;</span><span style="color: blue">&gt;</span><span style="color: blue">
            &lt;</span><span style="color: maroon">Columns</span><span style="color: blue">&gt; . . .</span><span style="color: blue">  </span><span style="color: blue">&lt;/</span><span style="color: maroon">Columns</span><span style="color: blue">&gt;
        &lt;/</span><span style="color: maroon">MasterTableView</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">RadGrid</span><span style="color: blue">&gt;
</span></p></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>Then in you’re DeleteCommand you can get you’re primary key value:</p>

<pre class="code"><span style="color: blue">protected void </span>customerOverviewRadGrid_DeleteCommand(<span style="color: blue">object </span>source, Telerik.Web.UI.<span style="color: #2b91af">GridCommandEventArgs </span>e)
{
    <span style="color: blue">int </span>id = (<span style="color: blue">int</span>)e.Item.OwnerTableView.DataKeyValues[e.Item.ItemIndex][<span style="color: #a31515">&quot;Id&quot;</span>];
    // run code to delete customer in the database . . . 
}</pre>
<a href="http://11011.net/software/vspaste"></a>
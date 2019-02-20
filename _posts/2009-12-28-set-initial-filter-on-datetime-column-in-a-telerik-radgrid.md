---
ID: 889
post_title: >
  Set initial filter on GridDateTimeColumn
  in a Telerik RadGrid
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/12/28/set-initial-filter-on-datetime-column-in-a-telerik-radgrid/
published: true
post_date: 2009-12-28 10:10:45
---
<p>If you want to set an initial filter on a Telerik RadGrid, use the “NeedDataSource” event and set the MasterTableView.FilterExpression and use the function MasterTableView.GetColumnSafe</p>  <pre class="code"><span style="color: blue">        protected void </span>RadGrid_NeedDataSource(<span style="color: blue">object </span>source, <span style="color: #2b91af">GridNeedDataSourceEventArgs </span>e)
        {
            <span style="color: green">// Set datasource here…
            </span>
            <span style="color: blue">if </span>(!IsPostBack)
            {
                <span style="color: green">// Set initial filter on [RadGrid]
                </span><span style="color: blue">this</span>.RadGrid.MasterTableView.FilterExpression = <span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;([Date] = '{0}')&quot;</span>, <span style="color: #2b91af">DateTime</span>.Today);

                <span style="color: green">// Set current filter function and value on [Date]
                </span><span style="color: #2b91af">GridColumn </span>column = <span style="color: blue">this</span>.RadGrid.MasterTableView.GetColumnSafe(<span style="color: #a31515">&quot;Date&quot;</span>);
                column.CurrentFilterFunction = <span style="color: #2b91af">GridKnownFunction</span>.EqualTo;
                column.CurrentFilterValue = <span style="color: #2b91af">DateTime</span>.Today.ToString();
            }
        }</pre>

<br />

<br />In the aspx page use “EqualTo” as filter, not “Contains” and use a GridDateTimeColumn not a GridBoundColumn

<br />

<br />

<pre class="code"><span style="color: blue">              &lt;</span><span style="color: #a31515">telerik</span><span style="color: blue">:</span><span style="color: #a31515">GridDateTimeColumn
                   </span><span style="color: red">DataField</span><span style="color: blue">=&quot;Date&quot;
                   </span><span style="color: red">HeaderText</span><span style="color: blue">=&quot;Date&quot;
                   </span><span style="color: red">SortExpression</span><span style="color: blue">=&quot;Date&quot;
                   </span><span style="color: red">UniqueName</span><span style="color: blue">=&quot;Date&quot;
                   </span><span style="color: red">FilterControlWidth</span><span style="color: blue">=&quot;70px&quot;
                   </span><span style="color: red">ShowFilterIcon</span><span style="color: blue">=&quot;false&quot;
                   </span><span style="color: red">DataType</span><span style="color: blue">=&quot;System.DateTime&quot;
                   </span><span style="color: red">CurrentFilterFunction</span><span style="color: blue">=&quot;EqualTo&quot;
                   </span><span style="color: red">PickerType</span><span style="color: blue">=&quot;DatePicker&quot;
                   </span><span style="color: red">AutoPostBackOnFilter</span><span style="color: blue">=&quot;true&quot;
                   </span><span style="color: red">HtmlEncode</span><span style="color: blue">=&quot;false&quot;
                   </span><span style="color: red">DataFormatString</span><span style="color: blue">=&quot;{0:dd-MM-yyyy}&quot;
                   </span><span style="color: #a31515">meta</span><span style="color: blue">:</span><span style="color: red">resourcekey</span><span style="color: blue">=&quot;Date&quot;&gt;
                   &lt;</span><span style="color: #a31515">ItemStyle </span><span style="color: red">Width</span><span style="color: blue">=&quot;70px&quot; /&gt;
               &lt;/</span><span style="color: #a31515">telerik</span><span style="color: blue">:</span><span style="color: #a31515">GridDateTimeColumn</span><span style="color: blue">&gt;</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<br />

<br /><a href="http://11011.net/software/vspaste"></a>
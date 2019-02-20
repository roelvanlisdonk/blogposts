---
ID: 891
post_title: 'Set initial sorting on a Telerik RadGrid  column'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/12/28/set-initial-sorting-on-a-telerik-radgrid-column/
published: true
post_date: 2009-12-28 11:11:58
---
<p>If you want to set an initial sorting on a column on a Telerik RadGrid, use the “NeedDataSource” event and add a GridSortExpression to the MasterTableView.SortExpressions</p>  <pre class="code"><span style="color: blue">        protected void </span>RadGrid_NeedDataSource(<span style="color: blue">object </span>source, <span style="color: #2b91af">GridNeedDataSourceEventArgs </span>e)
        {
            <span style="color: green">// Set datasource here…
            </span>
            <span style="color: blue">if </span>(!IsPostBack)
            {</pre>

<pre class="code"><span style="color: green">                // Clear the current sortexpressions
                </span><span style="color: blue">this</span>.RadGrid.MasterTableView.SortExpressions.Clear();

                <span style="color: green">// Create &quot;Date&quot; sorting
                </span><span style="color: #2b91af">GridSortExpression </span>expression = <span style="color: blue">new </span><span style="color: #2b91af">GridSortExpression</span>();
                expression.FieldName = <span style="color: #a31515">&quot;Date&quot;</span>;
                expression.SortOrder = <span style="color: #2b91af">GridSortOrder</span>.Descending;

                <span style="color: green">// Set initial sortexpression to the [Date] column
                </span><span style="color: blue">this</span>.opdrachtenRadGrid.MasterTableView.SortExpressions.AddSortExpression(expression);</pre>
<a href="http://11011.net/software/vspaste"></a>

<pre class="code">            }
        }</pre>

<br />

<br />In the aspx page:

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
<p>
  <br />Or you could use the “SortExpressions” tag in the MasterTableView tag:

  <br /></p>

<pre class="code"><p><span style="color: blue">&lt;</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">RadGrid 
        </span><span style="color: red">ID</span><span style="color: blue">=&quot;RadGrid1&quot;
</span><span style="color: blue">        </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;</span><span style="color: blue">&gt;
      </span><span style="color: blue"> &lt;</span><span style="color: maroon">MasterTableView</span><span style="color: blue">&gt;</span><span style="color: blue">
            &lt;</span><span style="color: maroon">SortExpressions</span><span style="color: blue">&gt;
               &lt;</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">GridSortExpression </span><span style="color: red">FieldName</span><span style="color: blue">=&quot;Name&quot; </span><span style="color: red">SortOrder</span><span style="color: blue">=&quot;Ascending&quot; /&gt;
            &lt;/</span><span style="color: maroon">SortExpressions</span><span style="color: blue">&gt;
            &lt;</span><span style="color: maroon">Columns</span><span style="color: blue">&gt;
                &lt;</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">GridBoundColumn 
                    </span><span style="color: red">AutoPostBackOnFilter</span><span style="color: blue">=&quot;true&quot;
                    </span><span style="color: red">CurrentFilterFunction</span><span style="color: blue">=&quot;Contains&quot;
                    </span><span style="color: red">DataField</span><span style="color: blue">=&quot;Name&quot;
                    </span><span style="color: red">FilterControlWidth</span><span style="color: blue">=&quot;200px&quot;
                    </span><span style="color: red">meta</span><span style="color: blue">:</span><span style="color: red">resourcekey</span><span style="color: blue">=&quot;CustomerNameColumn&quot; 
                    </span><span style="color: red">UniqueName</span><span style="color: blue">=&quot;Name&quot; 
                    </span><span style="color: red">SortExpression</span><span style="color: blue">=&quot;Name&quot;  
                    </span><span style="color: red">ShowFilterIcon</span><span style="color: blue">=&quot;true&quot;&gt;
                    &lt;</span><span style="color: maroon">ItemStyle </span><span style="color: red">Width</span><span style="color: blue">=&quot;200px&quot; /&gt;
                &lt;/</span><span style="color: maroon">telerik</span><span style="color: blue">:</span><span style="color: maroon">GridBoundColumn</span><span style="color: blue">&gt;</span></p><p><span style="color: blue">……</span></p></pre>
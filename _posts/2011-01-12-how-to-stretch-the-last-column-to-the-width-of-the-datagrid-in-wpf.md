---
ID: 1872
post_title: >
  How to stretch the last column to the
  width of the datagrid in WPF
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/01/12/how-to-stretch-the-last-column-to-the-width-of-the-datagrid-in-wpf/
published: true
post_date: 2011-01-12 13:50:31
---
<p>If you want to let the last column in a datagrid fill the datagrid, you should use the first columns width to auto en set the last column width to * and specify minimum widths for the columns:</p>  <pre class="code"><p><span style="color: blue">&lt;</span><span style="color: #a31515">DataGrid </span><span style="color: red">Name</span><span style="color: blue">=&quot;subsysteemSettingsDataGrid&quot; </span><span style="color: red">AutoGenerateColumns</span><span style="color: blue">=&quot;False&quot; </span><span style="color: red">HeadersVisibility</span><span style="color: blue">=&quot;Column&quot; </span><span style="color: red">HorizontalAlignment</span><span style="color: blue">=&quot;Stretch&quot; </span><span style="color: red">Margin</span><span style="color: blue">=&quot;10&quot; </span><span style="color: red">HorizontalGridLinesBrush</span><span style="color: blue">=&quot;LightGray&quot; </span><span style="color: red">VerticalGridLinesBrush</span><span style="color: blue">=&quot;LightGray&quot; </span><span style="color: red">HorizontalScrollBarVisibility</span><span style="color: blue">=&quot;Disabled&quot; </span><span style="color: red">CanUserAddRows</span><span style="color: blue">=&quot;False&quot; </span><span style="color: red">BorderBrush</span><span style="color: blue">=&quot;#FF8C8E94&quot; </span><span style="color: red">SelectionUnit</span><span style="color: blue">=&quot;FullRow&quot;  </span><span style="color: red">CellStyle</span><span style="color: blue">=&quot;{</span><span style="color: #a31515">StaticResource </span><span style="color: red">SelectedSubDataGridCellStyle</span><span style="color: blue">}&quot;&gt;
  &lt;</span><span style="color: #a31515">DataGrid.Columns</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">DataGridTextColumn </span><span style="color: red">Header</span><span style="color: blue">=&quot;Name&quot; </span><span style="color: red">Binding</span><span style="color: blue">=&quot;{</span><span style="color: #a31515">Binding </span><span style="color: red">Path</span><span style="color: blue">=Name, </span><span style="color: red">Mode</span><span style="color: blue">=TwoWay, <br /></span><span style="color: red">UpdateSourceTrigger</span><span style="color: blue">=PropertyChanged}&quot; </span><span style="color: red">MinWidth</span><span style="color: blue">=&quot;150&quot; </span><span style="color: red">Width</span><span style="color: blue">=&quot;Auto&quot; /&gt;
    &lt;</span><span style="color: #a31515">DataGridTextColumn </span><span style="color: red">Header</span><span style="color: blue">=&quot;Value&quot; </span><span style="color: red">Binding</span><span style="color: blue">=&quot;{</span><span style="color: #a31515">Binding </span><span style="color: red">Path</span><span style="color: blue">=Value, </span><span style="color: red">Mode</span><span style="color: blue">=TwoWay, <br /></span><span style="color: red">UpdateSourceTrigger</span><span style="color: blue">=PropertyChanged}&quot; </span><span style="color: red">MinWidth</span><span style="color: blue">=&quot;200&quot; </span><span style="color: red">Width</span><span style="color: blue">=&quot;*&quot; /&gt;
  &lt;/</span><span style="color: #a31515">DataGrid.Columns</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">DataGrid</span><span style="color: blue">&gt;
</span></p></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>De screendump below shows the last column stretched to the width of the datagrid</p>

<p>&#160;</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/01/image2.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/01/image_thumb2.png" width="751" height="122" /></a></p>
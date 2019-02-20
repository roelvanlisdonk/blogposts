---
ID: 3268
post_title: >
  How to add a CSS class to a kendo grid
  column
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/06/18/how-to-add-a-css-class-to-a-kendo-grid-column/
published: true
post_date: 2013-06-18 15:04:51
---
<p>If you want to add a class to a kendo grid column, use the columns.attributes:</p>  <p>&#160;</p>  <pre><code>&lt;div id=&quot;grid&quot;&gt;&lt;/div&gt;
&lt;script&gt;
$(&quot;#grid&quot;).kendoGrid({
  columns: [ {
    field: &quot;name&quot;,
    title: &quot;Name&quot;,
    attributes: {
      <font style="background-color: #ffff00">&quot;class&quot;: &quot;table-cell&quot;,</font>
      style: &quot;text-align: right; font-size: 14px&quot;
    }
  } ],
  dataSource: [ { name: &quot;Jane Doe&quot; }, { name: &quot;John Doe&quot; }]
});
&lt;/script&gt;</code></pre>

<p>&#160;</p>

<p><a href="http://docs.kendoui.com/api/web/grid">http://docs.kendoui.com/api/web/grid</a></p>
---
ID: 3273
post_title: >
  How to use a password field in a Kendo
  grid
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/06/19/how-to-use-a-password-field-in-a-kendo-grid/
published: true
post_date: 2013-06-19 14:48:23
---
<p>The demo at <a href="http://demos.kendoui.com/web/grid/editing-custom.html">http://demos.kendoui.com/web/grid/editing-custom.html</a> shows how to create a custom editor function. We can use this function to show a password field as editor in a Kendo grid.</p>  <pre class="code"><span style="background: white; color: blue">function </span><span style="background: white; color: black">passwordEditor(container, options)
{
    $(</span><span style="background: white; color: #a31515">'&lt;input type=&quot;password&quot; required data-bind=&quot;value:' </span><span style="background: white; color: black">+ options.field + </span><span style="background: white; color: #a31515">'&quot;/&gt;'</span><span style="background: white; color: black">).appendTo(container);
};</span></pre>

<p>In the column that should be used as password, use:</p>

<pre class="code"><span style="background: white; color: black">$(</span><span style="background: white; color: #a31515">&quot;#grid&quot;</span><span style="background: white; color: black">).kendoGrid({
    dataSource: dataSource,
    pageable: </span><span style="background: white; color: blue">true</span><span style="background: white; color: black">,
    height: 430,
    toolbar: [</span><span style="background: white; color: #a31515">&quot;create&quot;</span><span style="background: white; color: black">],
    columns: [
        { field: </span><span style="background: white; color: #a31515">&quot;ProductName&quot;</span><span style="background: white; color: black">, title: </span><span style="background: white; color: #a31515">&quot;Product Name&quot; </span><span style="background: white; color: black">},
        { field: </span><span style="background: white; color: #a31515">&quot;Category&quot;</span><span style="background: white; color: black">, title: </span><span style="background: white; color: #a31515">&quot;Category&quot;</span><span style="background: white; color: black">, width: </span><span style="background: white; color: #a31515">&quot;160px&quot;</span><span style="background: white; color: black">, editor: categoryDropDownEditor, template: </span><span style="background: white; color: #a31515">&quot;#=Category.CategoryName#&quot; </span><span style="background: white; color: black">},
        { field: </span><span style="background: white; color: #a31515">&quot;UnitPrice&quot;</span><span style="background: white; color: black">, title: </span><span style="background: white; color: #a31515">&quot;Unit Price&quot;</span><span style="background: white; color: black">, format: </span><span style="background: white; color: #a31515">&quot;{0:c}&quot;</span><span style="background: white; color: black">, width: </span><span style="background: white; color: #a31515">&quot;120px&quot; </span><span style="background: white; color: black">},
        { field: </span><span style="background: white; color: #a31515">&quot;UserPassword&quot;</span><span style="background: white; color: black">, title: </span><span style="background: white; color: #a31515">&quot;Password&quot;</span><span style="background: white; color: black">, editor: <font color="#ff0000">passwordEditor</font>, template: </span><span style="background: white; color: #a31515">&quot;…&quot; </span><span style="background: white; color: black">},
        { command: </span><span style="background: white; color: #a31515">&quot;destroy&quot;</span><span style="background: white; color: black">, title: </span><span style="background: white; color: #a31515">&quot; &quot;</span><span style="background: white; color: black">, width: </span><span style="background: white; color: #a31515">&quot;90px&quot; </span><span style="background: white; color: black">}],
    editable: </span><span style="background: white; color: blue">true
</span><span style="background: white; color: black">});</span></pre>

<p>&#160;</p>

<p>The template: &quot;…&quot; ensure no data is shown to the user, when the password is changed.</p>

<p>&#160;</p>

<p>An example would be:</p>

<p><font color="#a31515" face="Courier New"></font></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image15.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image_thumb15.png" width="580" height="107" /></a></p>
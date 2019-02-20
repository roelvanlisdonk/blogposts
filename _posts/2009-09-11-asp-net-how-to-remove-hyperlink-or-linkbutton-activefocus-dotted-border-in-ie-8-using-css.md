---
ID: 686
post_title: 'ASP.NET &#8211; How to remove hyperlink or linkbutton (active/focus) dotted border in IE 8 using CSS'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/09/11/asp-net-how-to-remove-hyperlink-or-linkbutton-activefocus-dotted-border-in-ie-8-using-css/
published: true
post_date: 2009-09-11 14:37:21
---
<p>When you set a border on a hyperlink in IE 8 it will display the border dotted when the hyperlink is clicked. In IE 6 and IE 7 the borders are not altered. To remove the dotted border when the hyperlink is active (has focus) in IE8 use the css attribute outline: none;   <br />    <br />&lt;a style=&quot;border-color: Red; border-style: solid; border-width: 1px; color: #000000; display: block;&quot; href=&quot;Default.aspx&quot;&gt;Link with dotted borders when clicked (active/focus) in IE8 &lt;/a&gt;    <br />    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; &lt;a style=&quot;border-color: Red; border-style: solid; border-width: 1px; color: #000000; display: block; <strong>outline: none</strong>;&quot; href=&quot;Default.aspx&quot;&gt;Link without dotted borders when clicked (active/focus) in IE8&lt;/a&gt;</p>
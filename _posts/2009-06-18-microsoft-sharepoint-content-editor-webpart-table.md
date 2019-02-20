---
ID: 555
post_title: 'Microsoft Sharepoint &#8211; Content Editor Webpart table'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/06/18/microsoft-sharepoint-content-editor-webpart-table/
published: true
post_date: 2009-06-18 09:27:16
---
<p>To use a standard styled table in the content editor webpart, use the following html code en paste the code in the “Source editor…” view of the content editor webpart.</p>  <p>&#160;</p>  <p>&lt;style type=&quot;text/css&quot;&gt;   <br />&#160;&#160;&#160; table.tableIssues { border-collapse: collapse; border: 1px solid #C0C0C0; margin-left: 10px; margin-top: 10px; }    <br />&#160;&#160;&#160; td.cellIssues { border: 1px solid #C0C0C0; }    <br />&lt;/style&gt;    <br />&lt;TABLE class=&quot;tableIssues&quot; cellSpacing=0 cellPadding=0&gt;    <br />&lt;TBODY&gt;    <br />&lt;TR&gt;    <br />&lt;TD class=&quot;cellIssues&quot; height=13 width=170&gt;&amp;nbsp;&lt;STRONG&gt;Subsysteem&lt;/STRONG&gt;&lt;/TD&gt;    <br />&lt;TD class=&quot;cellIssues&quot; height=13 width=200&gt;&lt;STRONG&gt;&amp;nbsp;Development&lt;/STRONG&gt;&lt;/TD&gt;    <br />&lt;TD class=&quot;cellIssues&quot; height=13 width=200&gt;&lt;STRONG&gt;Test&lt;/STRONG&gt;&lt;/TD&gt;&lt;/TR&gt;    <br />&lt;TR&gt;    <br />&lt;TD class=&quot;cellIssues&quot; width=170&gt;&amp;nbsp;Configuratorl&lt;/TD&gt;    <br />&lt;TD class=&quot;cellIssues&quot; width=200&gt;&amp;nbsp;Jan&lt;/TD&gt;    <br />&lt;TD class=&quot;cellIssues&quot; width=200&gt;&amp;nbsp;Piet&lt;/TD&gt;&lt;/TR&gt;    <br />&lt;TR&gt;    <br />&lt;TD class=&quot;cellIssues&quot; width=170&gt;&amp;nbsp;Database&lt;/TD&gt;    <br />&lt;TD class=&quot;cellIssues&quot; width=200&gt;&amp;nbsp;Jan&lt;/TD&gt;    <br />&lt;TD class=&quot;cellIssues&quot; width=200&gt;&amp;nbsp;Piet&lt;/TD&gt;&lt;/TR&gt;    <br />&lt;/TBODY&gt;&lt;/TABLE&gt;    </p>
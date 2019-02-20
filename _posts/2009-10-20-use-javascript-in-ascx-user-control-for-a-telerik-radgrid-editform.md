---
ID: 778
post_title: 'Use javascript in *.ascx user control for a Telerik RadGrid EditForm'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/10/20/use-javascript-in-ascx-user-control-for-a-telerik-radgrid-editform/
published: true
post_date: 2009-10-20 10:51:39
---
<p>If you use an *.ascx user control to add new rows to the Telerik RadGrid and want to use javascript dynamically loaded, you can use the Telerik “RadScriptBlock”:</p>  <pre class="code"><span style="color: blue">    &lt;</span><span style="color: #a31515">telerik</span><span style="color: blue">:</span><span style="color: #a31515">RadScriptBlock </span><span style="color: red">ID</span><span style="color: blue">=&quot;radScriptBlock&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
        &lt;</span><span style="color: #a31515">script </span><span style="color: red">language</span><span style="color: blue">=&quot;javascript&quot; </span><span style="color: red">type</span><span style="color: blue">=&quot;text/javascript&quot;&gt;
            </span>alert('Hello');
        <span style="color: blue">&lt;/</span><span style="color: #a31515">script</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">telerik</span><span style="color: blue">:</span><span style="color: #a31515">RadScriptBlock</span><span style="color: blue">&gt;</span></pre>
<a href="http://11011.net/software/vspaste"></a>
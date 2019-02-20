---
ID: 519
post_title: 'ASP .NET &#8211; How to add javascript script files to you&#039;re masterpage'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/06/09/asp-net-how-to-add-javascript-script-files-to-youre-masterpage/
published: true
post_date: 2009-06-09 14:10:07
---
<p>You can't add javascript script files to you're page header by using the normal &lt;link&gt; and &lt;script&gt; tags, when you are using masterpages in ASP .NET. <br />You will have to do this in the code behind files or use one of the following methods: <br /><br /><strong>Method 1 ASP .NET 1.1</strong></p><pre class="code"><span style="color: blue">&lt;</span><span style="color: #a31515">script </span><span style="color: red">src</span><span style="color: blue">='</span><span style="background: #ffee62">&lt;%</span>= this.ResolveUrl("~/scripts.js") <span style="background: #ffee62">%&gt;</span><span style="color: blue">' </span><span style="color: red">type</span><span style="color: blue">='text/javascript'&gt;&lt;/</span><span style="color: #a31515">script</span><span style="color: blue">&gt;<br /></span></pre><pre class="code"><span style="color: blue"></pre></span>
<p><br /><br /><strong>Method 2 Using the ajax script manager</strong> </p><pre class="code"><span style="color: blue">&lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">ScriptManager </span><span style="color: red">ID</span><span style="color: blue">="ScriptManager1" </span><span style="color: red">runat</span><span style="color: blue">="server" </span><span style="color: red">EnablePartialRendering</span><span style="color: blue">="true" &gt;
                &lt;</span><span style="color: #a31515">Scripts</span><span style="color: blue">&gt;
                    &lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">ScriptReference </span><span style="color: red">Path</span><span style="color: blue">="~/Script/Master.js" /&gt;
                &lt;/</span><span style="color: #a31515">Scripts</span><span style="color: blue">&gt;
            &lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">ScriptManager</span><span style="color: blue">&gt;</span></pre><pre class="code"><span style="color: blue"></span></pre><a href="http://11011.net/software/vspaste"></a>
<p><br />I used the second method.<br /><br /><br />Solution found at: <a title="http://forums.asp.net/t/987646.aspx" href="http://forums.asp.net/t/987646.aspx">http://forums.asp.net/t/987646.aspx</a></p>
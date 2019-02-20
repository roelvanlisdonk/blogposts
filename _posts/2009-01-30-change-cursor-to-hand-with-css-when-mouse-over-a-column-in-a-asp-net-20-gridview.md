---
ID: 241
post_title: >
  Change cursor to hand with CSS, when
  mouse over a column in a ASP .NET 2.0
  GridView
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/01/30/change-cursor-to-hand-with-css-when-mouse-over-a-column-in-a-asp-net-20-gridview/
published: true
post_date: 2009-01-30 08:25:20
---
<pre class="code">When you want to change the cursor to a hand instead of the default pointer on mouse over, use CSS.</pre><pre class="code">In you're gridview column:</pre><pre class="code"><span style="color:blue;">&lt;</span><span style="color:#a31515;">Columns</span><span style="color:blue;">&gt;
      &lt;</span><span style="color:#a31515;">asp</span><span style="color:blue;">:</span><span style="color:#a31515;">TemplateField </span><span style="color:red;">HeaderText</span><span style="color:blue;">="Barcode"&gt;
           &lt;</span><span style="color:#a31515;">ItemTemplate</span><span style="color:blue;">&gt;&lt;</span><span style="color:#a31515;">span </span><span style="color:red;">class</span><span style="color:blue;">="hand"&gt;</span><span style="background:#ffee62;">&lt;%</span><span style="color:blue;"># </span>Eval(<span style="color:#a31515;">"Column"</span>)<span style="background:#ffee62;">%&gt;</span><span style="color:blue;">&lt;/</span><span style="color:#a31515;">span</span><span style="color:blue;">&gt;&lt;/</span><span style="color:#a31515;">ItemTemplate</span><span style="color:blue;">&gt;
      &lt;/</span><span style="color:#a31515;">asp</span><span style="color:blue;">:</span><span style="color:#a31515;">TemplateField</span><span style="color:blue;">&gt;
</span><span style="color:blue;">&lt;/</span><span style="color:#a31515;">Columns</span><span style="color:blue;">&gt;</span></pre><a href="http://11011.net/software/vspaste"></a><pre class="code"><span style="color:blue;"><font color="#000000">In the header:</font></span></pre>
<p><pre class="code"><span style="color:green;"></span></pre><a href="http://11011.net/software/vspaste"></a><span style="color:blue;">&lt;</span><span style="color:#a31515;">style </span><span style="color:red;">type</span><span style="color:blue;">="text/css"&gt;<br />&nbsp;&nbsp;&nbsp; </span><span style="color:#a31515;">.hand </span>{ <span style="color:red;">cursor</span>: <span style="color:blue;">pointer</span>; <span style="color:red;">cursor</span>: <span style="color:blue;">hand</span>; } <span style="color:green;">/* cross browser hand */<br /></span><span style="color:blue;">&lt;/</span><span style="color:#a31515;">style</span><span style="color:blue;">&gt;</span></p><a href="http://11011.net/software/vspaste"></a>
<p><span style="background:yellow;color:blue;"><font face="Courier New"></font></span>&nbsp;</p>
<p><span style="background:yellow;color:blue;"><font face="Courier New"></font>&nbsp;</p><pre class="code"><br /><br /><br /><br /><br /><br /><br /></pre><a href="http://11011.net/software/vspaste"></a></span>
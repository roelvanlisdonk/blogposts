---
ID: 2284
post_title: 'How to preserve leading spaces in a DropDownList in HTML and C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/12/12/how-to-preserve-leading-spaces-in-a-dropdownlist-in-html-and-c/
published: true
post_date: 2011-12-12 11:20:37
---
<p>If you want to show a hierarchy of data in a DropDownlist by using spaces in front of each item, then you will find that normal spaces don’t work, instead use &amp;nbsp; and Server.HtmlDecode().</p>  <p>&#160;</p>  <p>&#160;</p>  <pre class="code"><span style="color: blue">namespace </span>WebApplication1
{
    <span style="color: blue">public partial class </span><span style="color: #2b91af">_Default </span>: System.Web.UI.<span style="color: #2b91af">Page
    </span>{
        <span style="color: blue">protected void </span>Page_Load(<span style="color: blue">object </span>sender, <span style="color: #2b91af">EventArgs </span>e)
        {
            DropDownList1.Items.Clear();
            DropDownList1.Items.Add(<span style="color: #a31515">&quot;Level 1&quot;</span>);
            DropDownList1.Items.Add(<span style="color: #a31515">&quot;  Level 2&quot;</span>);
            DropDownList1.Items.Add(<span style="color: #a31515">&quot;    Level 3&quot;</span>);
            DropDownList1.Items.Add(<span style="color: #a31515">&quot;      Level 4&quot;</span>);
        }
    }
}</pre>


<p>No hierarchy!!!</p>

<p>&#160;</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/12/image5.png" rel="lightbox"><img style="background-image: none; border-right-width: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/12/image_thumb5.png" width="580" height="345" /></a></p>

<p>&#160;</p>

<pre class="code"><span style="color: blue">namespace </span>WebApplication1
{
    <span style="color: blue">public partial class </span><span style="color: #2b91af">_Default </span>: System.Web.UI.<span style="color: #2b91af">Page
    </span>{
        <span style="color: blue">protected void </span>Page_Load(<span style="color: blue">object </span>sender, <span style="color: #2b91af">EventArgs </span>e)
        {
            DropDownList1.Items.Clear();
            DropDownList1.Items.Add(Server.HtmlDecode(<span style="color: #a31515">&quot;Level 1&quot;</span>.Replace(<span style="color: #a31515">&quot; &quot;</span>, <span style="color: #a31515">&quot;&amp;nbsp;&quot;</span>)));
            DropDownList1.Items.Add(Server.HtmlDecode(<span style="color: #a31515">&quot;  Level 2&quot;</span>.Replace(<span style="color: #a31515">&quot; &quot;</span>, <span style="color: #a31515">&quot;&amp;nbsp;&quot;</span>)));
            DropDownList1.Items.Add(Server.HtmlDecode(<span style="color: #a31515">&quot;    Level 3&quot;</span>.Replace(<span style="color: #a31515">&quot; &quot;</span>, <span style="color: #a31515">&quot;&amp;nbsp;&quot;</span>)));
            DropDownList1.Items.Add(Server.HtmlDecode(<span style="color: #a31515">&quot;      Level 4&quot;</span>.Replace(<span style="color: #a31515">&quot; &quot;</span>, <span style="color: #a31515">&quot;&amp;nbsp;&quot;</span>)));
        }
    }
}</pre>


<p>Now with hierarchy!!!</p>

<p>&#160;</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/12/image6.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/12/image_thumb6.png" width="572" height="423" /></a></p>
---
ID: 289
post_title: 'Setting the GridView PagerStyle height in ASP .NET 2.0 with C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/03/18/setting-the-gridview-pagerstyle-height-in-asp-net-20-with-c/
published: true
post_date: 2009-03-18 08:46:32
---
<p>When you set the PagerStyle Height property this will no allways set the correct height of the PageStyle.</p><a href="http://11011.net/software/vspaste"></a><pre class="code"><span style="color:blue;">&lt;</span><span style="color:#a31515;">asp</span><span style="color:blue;">:</span><span style="color:#a31515;">GridView </span><span style="color:red;">ID</span><span style="color:blue;">="Test"&gt;
    &lt;</span><span style="color:#a31515;">PagerStyle  </span><span style="color:red;">Height</span><span style="color:blue;">="10px" /&gt;
&lt;/</span><span style="color:#a31515;">asp</span><span style="color:blue;">:</span><span style="color:#a31515;">GridView</span><span style="color:blue;">&gt;</span></pre><a href="http://11011.net/software/vspaste"></a>
<p><br /><br />To set the correct height use a CSS class:</p><pre class="code"><span style="color:blue;">&lt;</span><span style="color:#a31515;">asp</span><span style="color:blue;">:</span><span style="color:#a31515;">GridView </span><span style="color:red;">ID</span><span style="color:blue;">="Test"&gt;
    &lt;</span><span style="color:#a31515;">PagerStyle  </span><span style="color:red;">CssClass</span><span style="color:blue;">="PagerStyle" /&gt;
&lt;/</span><span style="color:#a31515;">asp</span><span style="color:blue;">:</span><span style="color:#a31515;">GridView</span><span style="color:blue;">&gt;</span></pre><a href="http://11011.net/software/vspaste"></a>
<p><br />In you're CSS file add:<br /><br /></p><pre class="code"><span style="color:#a31515;">TR.PagerStyle TD
</span>{
    <span style="color:red;">height</span>: <span style="color:blue;">10px</span>;
    <span style="color:red;">margin</span>: <span style="color:blue;">0px</span>;
    <span style="color:red;">padding-top</span>: <span style="color:blue;">2px</span>;
    <span style="color:red;">padding-bottom</span>: <span style="color:blue;">2px</span>;
}
<span style="color:#a31515;">TR.PagerStyle TD TABLE
</span>{
    <span style="color:red;">margin</span>: <span style="color:blue;">0px</span>;
    <span style="color:red;">padding-top</span>: <span style="color:blue;">2px</span>;
    <span style="color:red;">padding-bottom</span>: <span style="color:blue;">2px</span>;
}</pre><a href="http://11011.net/software/vspaste"></a>
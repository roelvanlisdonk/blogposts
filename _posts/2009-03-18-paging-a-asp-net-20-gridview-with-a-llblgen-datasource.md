---
ID: 294
post_title: >
  Paging a ASP .NET 2.0 GridView with a
  LLBLGEN datasource
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/03/18/paging-a-asp-net-20-gridview-with-a-llblgen-datasource/
published: true
post_date: 2009-03-18 08:55:39
---
<p>If you want to allow paging in a ASP .NET 2.0 GridView that uses a LLBLGEN datasource:</p> <p>- set AllowPaging = True<br /><br /><br /><a href="http://roelvanlisdonk.files.wordpress.com/2009/03/image.png"><img style="border-right:0;border-top:0;border-left:0;border-bottom:0;" height="312" alt="image" src="http://roelvanlisdonk.files.wordpress.com/2009/03/image-thumb.png" width="325" border="0"></a> </p> <p> <a href="http://roelvanlisdonk.files.wordpress.com/2009/03/image2.png"><img style="border-right:0;border-top:0;border-left:0;border-bottom:0;" height="319" alt="image" src="http://roelvanlisdonk.files.wordpress.com/2009/03/image-thumb2.png" width="328" border="0"></a><br /></p> <p>- Create the PageIndexChanging event</p> <blockquote><pre class="code"><span style="color:gray;">/// &lt;summary&gt;
/// </span><span style="color:green;">Change the page of the GridViewKlanten
</span><span style="color:gray;">/// &lt;/summary&gt;
/// &lt;param name="sender"&gt;&lt;/param&gt;
/// &lt;param name="e"&gt;&lt;/param&gt;
</span><span style="color:blue;">protected void </span>GridViewKlanten_PageIndexChanging(<span style="color:blue;">object </span>sender, <span style="color:#2b91af;">GridViewPageEventArgs </span>e)
{
    GridViewKlanten.PageIndex = e.NewPageIndex;
    GridviewKlantenBind();
<span style="color:gray;"></span><span style="color:gray;"></span>}</pre></blockquote><pre class="code"><span style="color:gray;">       /// &lt;summary&gt;
       /// </span><span style="color:green;">Get klanten from database and bind to GridView
       </span><span style="color:gray;">/// &lt;/summary&gt;
       </span><span style="color:blue;">private void </span>GridviewKlantenBind()
       {
           <span style="color:#2b91af;">KlantComponent </span>klantcompent = <span style="color:blue;">new </span><span style="color:#2b91af;">KlantComponent</span>(_logger);
           GridViewKlanten.DataSource = klantcompent.GetKlanten();
           GridViewKlanten.DataBind();
       }</pre><pre class="code">&nbsp;</pre><pre class="code"><strong>Don't forget to rebind the GridView or you will not see any change.</strong></pre><pre class="code">
</pre><a href="http://11011.net/software/vspaste"></a><a href="http://11011.net/software/vspaste"></a>
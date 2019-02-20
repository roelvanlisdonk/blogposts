---
ID: 1203
post_title: 'How to get all categories from the master category list in Outlook 2010 with C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/04/07/how-to-get-all-categories-from-the-master-category-list-in-outlook-2010-with-c/
published: true
post_date: 2010-04-07 16:56:38
---
<p>If you want the get all categories from the master category list in Outlook 2010, use the Session object from the application:   <br /></p>  <pre class="code"><span style="color: #2b91af">            Categories </span>categories = <span style="color: #2b91af">Globals</span>.ThisAddIn.Application.Session.Categories;
            <span style="color: blue">foreach </span>(<span style="color: #2b91af">Category </span>category <span style="color: blue">in </span>categories)
            {
                <span style="color: blue">string </span>name = category.Name;
            }</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>This will list all categories from the dialog “All Categories…”:</p>

<p>&#160;</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/04/image8.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/04/image_thumb8.png" width="504" height="392" /></a></p>
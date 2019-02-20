---
ID: 688
post_title: 'ASP .NET &#8211; Get page filename from request url'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/09/14/asp-net-get-page-filename-from-request-url/
published: true
post_date: 2009-09-14 08:46:51
---
<p>If you want to get the page filename from the current request url in ASP .NET you can use:   <br /><span style="color: #2b91af"></span>    <pre class="code"><span style="color: blue">string </span>page = <span style="color: #2b91af">Path</span>.GetFileName(Request.Url.LocalPath).ToLower();</pre>
  <a href="http://11011.net/software/vspaste"></a>

  <p>
    <br />This can be used to switch logica in de master page.

    <br /><span style="color: #2b91af">
      <br />

      <br /></span></p>

  <p>
    <br /></p>
  <a href="http://11011.net/software/vspaste"></a></p>
---
ID: 1010
post_title: >
  Do a postback from javascript with ASP
  .NET AJAX
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/02/08/do-a-postback-from-javascript-with-asp-net-ajax/
published: true
post_date: 2010-02-08 15:45:12
---
<p>If you want to do a postback from javascript with ASP .NET AJAX and the aspx page contains a</p>  <pre class="code"><span style="color: blue">&lt;</span><span style="color: #a31515">form </span><span style="color: red">id</span><span style="color: blue">=&quot;mainForm&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>, you can create and use the javascript function to do a postback from javascript:
  <br /><span style="color: blue">
    <br />function </span>DoPostBack() {

  <br />&#160;&#160;&#160; <span style="color: blue">var </span>form = document.getElementById(<span style="color: #a31515">'mainForm'</span>);

  <br />&#160;&#160;&#160; form.submit();

  <br />}</p>
<a href="http://11011.net/software/vspaste"></a>
---
ID: 2492
post_title: 'MVC tip: use Url.Content in script src attribute, in *.cshtml files!'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/02/07/mvc-tip-use-url-content-in-your-script-src-attribute/
published: true
post_date: 2012-02-07 10:58:12
---
<p>In your &quot;*.cshtml&quot; pages, use Url.Content and don’t directly specify the locations of the JavaScript files, because specifying the JavaSript files directly will result in 404 error, when using a virtual directory/application within a IIS website.</p>  <p>&#160;</p>  <p>So use   <pre class="code"><span style="color: blue">&lt;!</span><span style="color: maroon">DOCTYPE </span><span style="color: red">html</span><span style="color: blue">&gt;
&lt;</span><span style="color: maroon">html</span><span style="color: blue">&gt;
&lt;</span><span style="color: maroon">head</span><span style="color: blue">&gt;
    &lt;</span><span style="color: maroon">title</span><span style="color: blue">&gt;</span><span style="background: yellow">@</span>ViewBag.Title<span style="color: blue">&lt;/</span><span style="color: maroon">title</span><span style="color: blue">&gt;
    &lt;</span><span style="color: maroon">link </span><span style="color: red">href</span><span style="color: blue">=&quot;</span><span style="background: yellow">@</span><span style="color: blue">Url.Content(</span><span style="color: #a31515">&quot;~/Content/Site.css&quot;</span><span style="color: blue">)&quot; </span><span style="color: red">rel</span><span style="color: blue">=&quot;stylesheet&quot; </span><span style="color: red">type</span><span style="color: blue">=&quot;text/css&quot; /&gt;
    &lt;</span><span style="color: maroon">script </span><span style="color: red">src</span><span style="color: blue">=&quot;</span><span style="background: yellow">@</span><span style="color: blue">Url.Content(</span><span style="color: #a31515">&quot;~/Scripts/jquery-1.4.4.min.js&quot;</span><span style="color: blue">)&quot; </span><span style="color: red">type</span><span style="color: blue">=&quot;text/javascript&quot;&gt;&lt;/</span><span style="color: maroon">script</span><span style="color: blue">&gt;
&lt;/</span><span style="color: maroon">head</span><span style="color: blue">&gt;
</span></pre>
  and don’t use:

  <pre class="code"><span style="color: blue">&lt;!</span><span style="color: maroon">DOCTYPE </span><span style="color: red">html</span><span style="color: blue">&gt;
&lt;</span><span style="color: maroon">html</span><span style="color: blue">&gt;
&lt;</span><span style="color: maroon">head</span><span style="color: blue">&gt;
    &lt;</span><span style="color: maroon">title</span><span style="color: blue">&gt;</span><span style="background: yellow">@</span>ViewBag.Title<span style="color: blue">&lt;/</span><span style="color: maroon">title</span><span style="color: blue">&gt;
    &lt;</span><span style="color: maroon">link </span><span style="color: red">href</span><span style="color: blue">=&quot;</span><span style="color: #a31515">/Content/Site.css</span><span style="color: blue">&quot; </span><span style="color: red">rel</span><span style="color: blue">=&quot;stylesheet&quot; </span><span style="color: red">type</span><span style="color: blue">=&quot;text/css&quot; /&gt;
    &lt;</span><span style="color: maroon">script </span><span style="color: red">src</span><span style="color: blue">=&quot;/</span><span style="color: #a31515">Scripts/jquery-1.4.4.min.js</span><span style="color: blue">&quot; </span><span style="color: red">type</span><span style="color: blue">=&quot;text/javascript&quot;&gt;&lt;/</span><span style="color: maroon">script</span><span style="color: blue">&gt;
&lt;/</span><span style="color: maroon">head</span><span style="color: blue">&gt;
</span></pre></p>
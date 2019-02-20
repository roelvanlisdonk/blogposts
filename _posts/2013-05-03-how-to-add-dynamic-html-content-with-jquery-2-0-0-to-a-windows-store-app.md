---
ID: 3210
post_title: >
  How to add dynamic html content with
  jQuery 2.0.0 to a Windows Store app.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/05/03/how-to-add-dynamic-html-content-with-jquery-2-0-0-to-a-windows-store-app/
published: true
post_date: 2013-05-03 14:42:42
---
<p>If you directly append html to the DOM that contains HTLM 5 data attributes or event handlers, like the onclick event to a Windows store app, you might get the exception during runtime:</p>  <p align="left">&#160;</p>  <p align="left">Unhandled exception at line 5, column 18611 in ms-appx://3bce315e-3d91-43e6-8149-06d6377f04a1/js/libraries/jquery-2.0.0.min.js</p>  <p align="left">0x800c001c - JavaScript runtime error: Unable to add dynamic content. A script attempted to inject dynamic content, or elements previously modified dynamically, that might be unsafe. For example, using the innerHTML property to add script or malformed HTML will generate this exception. Use the toStaticHTML method to filter dynamic content, or explicitly create elements and attributes with a method such as createElement.&#160; For more information, see <a href="http://go.microsoft.com/fwlink/?LinkID=247104">http://go.microsoft.com/fwlink/?LinkID=247104</a>.</p>  <p>&#160;</p>  <p>This exception even crashes my Windows Store app, because it is not caught anywhere in the code.</p>  <p>&#160;</p>  <p>In my case this was caused by the following code:</p>  <pre class="code"><span style="background: white; color: blue">var </span><span style="background: white; color: black">content = </span><span style="background: white; color: #a31515">&quot;&quot;</span><span style="background: white; color: black">;
content += </span><span style="background: white; color: #a31515">' &lt;ul data-val=&quot;users&quot; onclick=&quot;console.log(\'Clicked on users list.\');&quot;&gt; '</span><span style="background: white; color: black">;
content += </span><span style="background: white; color: #a31515">' &lt;li&gt;User1&lt;/li&gt; '</span><span style="background: white; color: black">;
content += </span><span style="background: white; color: #a31515">' &lt;/ul&gt; '</span><span style="background: white; color: black">;

</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">container = $(</span><span style="background: white; color: #a31515">'#content'</span><span style="background: white; color: black">);
container.empty();
container.append(content);</span></pre>


<p>This can be fixed by using jQuery document fragments:</p>

<pre class="code"><span style="background: white; color: blue">var </span><span style="background: white; color: black">ul = $(</span><span style="background: white; color: #a31515">'&lt;ul&gt;'</span><span style="background: white; color: black">, { </span><span style="background: white; color: #a31515">'data-val'</span><span style="background: white; color: black">: </span><span style="background: white; color: #a31515">'listOfNames'</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">'onclick'</span><span style="background: white; color: black">: </span><span style="background: white; color: #a31515">'console.log(&quot;Clicked on users list.&quot;);' </span><span style="background: white; color: black">});
ul.append(</span><span style="background: white; color: #a31515">'&lt;li&gt;' </span><span style="background: white; color: black">+ </span><span style="background: white; color: #a31515">'User1' </span><span style="background: white; color: black">+ </span><span style="background: white; color: #a31515">'&lt;/li&gt;'</span><span style="background: white; color: black">);

</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">container = $(</span><span style="background: white; color: #a31515">'#content'</span><span style="background: white; color: black">);
container.empty();
container.append(ul);</span></pre>


<p>&#160;</p>

<p>For more information on globally killing this exception, without changing the code (not recommended), see</p>

<p><a href="http://blog.jonathanchannon.com/2013/01/24/using-angularjsbackbonejs-in-windows-8-javascript-app/">http://blog.jonathanchannon.com/2013/01/24/using-angularjsbackbonejs-in-windows-8-javascript-app/</a></p>

<p>It uses jQuery.isUnsafe = true; so all calls to .append and appendTo are wrapped with Microsoft's MSApp.execUnsafeLocalFunction.</p>
---
ID: 2509
post_title: >
  How to add a CSS class to a HTML
  element, only when not present, by using
  jQuery.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/02/28/how-to-add-a-css-class-to-a-html-element-only-when-not-present-by-using-jquery/
published: true
post_date: 2012-02-28 11:39:24
---
<p>You can add a CSS class to a HTML element, only when this class is not present on the HTML element, by using the jQuery function .toggleClass and using the switch parameter:</p>  <p>If your HTML page contains a div like:</p>  <pre class="code"><span style="color: blue">&lt;</span><span style="color: maroon">div </span><span style="color: red">id</span><span style="color: blue">=&quot;title&quot;&gt;
</span>...
<span style="color: blue">&lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
</span></pre>


<p>Adding the JavaScript code:
  <pre class="code">$(document).ready(<span style="color: blue">function </span>()
{
    <span style="color: #006400">// The CSS class &quot;titleStyling&quot;, will now be added, because it is does not exist on the title yet.
    </span>$(<span style="color: maroon">&quot;#title&quot;</span>).toggleClass(<span style="color: maroon">&quot;titleStyling&quot;</span>, <span style="color: blue">true</span>);

    <span style="color: #006400">// Subsequent calls will not add extra classes, where the jQuery .addClass will.
    </span>$(<span style="color: maroon">&quot;#title&quot;</span>).toggleClass(<span style="color: maroon">&quot;titleStyling&quot;</span>, <span style="color: blue">true</span>);

    <span style="color: #006400">// Subsequent calls will not add extra classes, where the jQuery .addClass will.
    </span>$(<span style="color: maroon">&quot;#title&quot;</span>).toggleClass(<span style="color: maroon">&quot;titleStyling&quot;</span>, <span style="color: blue">true</span>);
});</pre>
  Will result in

  <pre class="code"><span style="color: blue">&lt;</span><span style="color: maroon">div </span><span style="color: red">id</span><span style="color: blue">=&quot;title&quot; </span><span style="color: red">class</span><span style="color: blue">=&quot;titleStyling&quot;&gt;
</span>...          
<span style="color: blue">&lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;
</span></pre></p>
---
ID: 2497
post_title: >
  How to clear all canvases found in a div
  with jQuery
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/02/10/how-to-clear-all-canvases-found-in-a-div-with-jquery/
published: true
post_date: 2012-02-10 14:55:02
---
<p>&#160;</p>  <p>If you want to clear all canvases found in a given div with jQuery, you can use the following code:</p>  <pre class="code"><span style="color: #006400">    // Clear all canvases found in the given div, including all child canvases and sub child canvases.
    </span>$(<span style="color: maroon">'#DivToFind canvas'</span>).each(<span style="color: blue">function</span>(idx, item) {
        <span style="color: blue">var </span>context = item.getContext(<span style="color: maroon">&quot;2d&quot;</span>);
        context.clearRect(0, 0, item.width, item.height);
        context.beginPath();        
    });</pre>
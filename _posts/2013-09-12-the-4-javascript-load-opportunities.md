---
ID: 3438
post_title: The 4 JavaScript load opportunities
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/09/12/the-4-javascript-load-opportunities/
published: true
post_date: 2013-09-12 08:53:54
---
<p>Interesting podcast by Scott Hanselman and Nicholas Zakas:</p>  <p><a href="http://hanselminutes.com/383/enough-with-the-javascript-already-with-nicholas-zakas">http://hanselminutes.com/383/enough-with-the-javascript-already-with-nicholas-zakas</a></p>  <p>&#160;</p>  <p>It mentions the 4 JavaScript load opportunities:</p>  <ol>   <li>In the &lt;head&gt; tag</li>    <li>Before the &lt;/body&gt; tag</li>    <li>After page load (windows.onload DOM ready function)</li>    <li>On demand (when user clicks a button, mouse is 100px from button, user types first letter etc.)</li> </ol>  <p>&#160;</p>  <p>For performance reasons, use 4, then 3, then 2 and if you can’t do without, use 1.</p>
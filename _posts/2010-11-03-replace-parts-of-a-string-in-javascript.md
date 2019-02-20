---
ID: 1793
post_title: Replace parts of a string in JavaScript
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/11/03/replace-parts-of-a-string-in-javascript/
published: true
post_date: 2010-11-03 15:44:37
---
<p>If you want to find and replace parts of a string in JavaScript, you can use the replace function:</p>  <p>&#160;</p>  <p><strong>Code</strong></p>  <p>var str = &quot;This is Microsoft&quot;</p>  <p>str = str.replace(&quot;Microsoft&quot;, &quot;ADA ICT&quot;);</p>  <p>document.write(str);</p>  <p>&#160;</p>  <p><strong>Output</strong></p>  <p>This is ADA ICT</p>
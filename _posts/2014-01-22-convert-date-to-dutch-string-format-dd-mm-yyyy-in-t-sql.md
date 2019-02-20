---
ID: 3675
post_title: 'Convert date to &quot;Dutch&quot; string format &quot;dd-mm-yyyy&quot; in T-SQL'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/01/22/convert-date-to-dutch-string-format-dd-mm-yyyy-in-t-sql/
published: true
post_date: 2014-01-22 16:40:02
---
<p>If you want to convert a date to a string in the format &quot;dd-mm-yyyy&quot; in T-SQL, you can use the following code:</p>  <p>&#160;</p>  <pre class="code"><span style="color: blue">declare </span><span style="color: teal">@Now </span><span style="color: blue">date </span><span style="color: gray">= </span><span style="color: red">'2014-01-22'
</span><span style="color: blue">select </span><span style="color: magenta">convert</span><span style="color: gray">(</span><span style="color: blue">varchar</span><span style="color: gray">(</span>10<span style="color: gray">), </span><span style="color: teal">@Now</span><span style="color: gray">, </span>105<span style="color: gray">)
</span></pre>

<p><strong>Result</strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/01/image12.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/01/image_thumb12.png" width="171" height="110" /></a></p>
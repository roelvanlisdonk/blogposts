---
ID: 5062
post_title: 'Fixing kendo.drawing.drawDOM in IE9: Unable to get property &#8216;add&#8217; of undefined or null reference.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2017/02/02/fixing-kendo-drawing-drawdom-in-ie9-unable-to-get-property-add-of-undefined-or-null-reference/
published: true
post_date: 2017-02-02 15:53:54
---
<pre>



I was getting the error:
Unable to get property 'add' of undefined or null reference.
, when calling kendo.drawing.drawDOM in IE9 with kendo 2017.1.118

This was fixed by using the polyfill: https://github.com/eligrey/classList.js



</pre>
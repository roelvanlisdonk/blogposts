---
ID: 4321
post_title: 'How to fix: can&rsquo;t type in textbox inside kendo sortable'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/04/29/how-to-fix-cant-type-in-textbox-inside-kendo-sortable/
published: true
post_date: 2015-04-29 10:38:39
---
<p>I had some input type=”text” html elements inside a kendo sortable. These textboxes couldn’t get focus, I was unable to type in the textbox, due to the fact it was inside a “draggable” element.</p>  <p>(first I thought it was the css property “user-select”, but that was not the case).</p>  <p>&#160;</p>  <p>The fix is documented on the kendo api site: </p>  <p><a title="http://docs.telerik.com/kendo-ui/web/sortable/overview#sortable-widget-with-focus-able-input-elements" href="http://docs.telerik.com/kendo-ui/web/sortable/overview#sortable-widget-with-focus-able-input-elements">http://docs.telerik.com/kendo-ui/web/sortable/overview#sortable-widget-with-focus-able-input-elements</a></p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/04/image.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/04/image_thumb.png" width="580" height="237" /></a></p>
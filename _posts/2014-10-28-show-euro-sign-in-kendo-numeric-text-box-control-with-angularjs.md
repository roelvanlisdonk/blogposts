---
ID: 4085
post_title: >
  Show euro sign in kendo numeric text box
  control with AngularJS.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/10/28/show-euro-sign-in-kendo-numeric-text-box-control-with-angularjs/
published: true
post_date: 2014-10-28 11:41:01
---
<p>Here’s a plunker demonstrating a kendo numeric text box with euro sign in it, bound to AngularJS.</p> <p><a title="http://plnkr.co/edit/z2jpoZ3WQRmHxwnhIF4G?p=preview" href="http://plnkr.co/edit/z2jpoZ3WQRmHxwnhIF4G?p=preview">http://plnkr.co/edit/z2jpoZ3WQRmHxwnhIF4G?p=preview</a></p> <p>&nbsp;</p> <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/10/image7.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/10/image_thumb7.png" width="580" height="167"></a></p> <p>&nbsp;</p><pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">input </span><span style="background: white; color: red">kendo-numeric-text-box k-min</span><span style="background: white; color: blue">="0" </span><span style="background: white; color: red">k-format</span><span style="background: white; color: blue">="'c0'" </span><span style="background: white; color: red">k-ng-model</span><span style="background: white; color: blue">="totalCost" </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">="text" /&gt;</span></pre>
<p>&nbsp;</p>
<p><strong><font size="3">Main pitfall is the single quotes inside the k-format</font></strong></p><pre class="code"></pre>
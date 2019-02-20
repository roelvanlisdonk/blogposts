---
ID: 4250
post_title: >
  How to validate an entered text to a min
  date in a kendo datepicker in AngularJS.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/01/22/how-to-validate-an-entered-text-to-a-min-date-in-a-kendo-datepicker-in-angularjs/
published: true
post_date: 2015-01-22 11:10:00
---
<p>The code and live preview can be found here:</p>  <p><a title="http://plnkr.co/edit/jdnRjO?p=preview" href="http://plnkr.co/edit/jdnRjO?p=preview">http://plnkr.co/edit/jdnRjO?p=preview</a></p>  <p>&#160;</p>  <p>When no date is entered a “pink” border will be shown:</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/01/image5.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/01/image_thumb5.png" width="398" height="313" /></a></p>  <p>&#160;</p>  <p>When a date is entered that’s before the “min” date a “pink” border will be shown:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/01/image6.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/01/image_thumb6.png" width="438" height="308" /></a></p>  <p>&#160;</p>  <p>When a date on or after the min date is entered, no border will be shown:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/01/image7.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/01/image_thumb7.png" width="423" height="287" /></a></p>
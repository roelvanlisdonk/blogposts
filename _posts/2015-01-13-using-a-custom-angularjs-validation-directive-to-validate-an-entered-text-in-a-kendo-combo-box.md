---
ID: 4238
post_title: >
  Using a custom AngularJS validation
  directive to validate an entered text in
  a kendo combo box.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/01/13/using-a-custom-angularjs-validation-directive-to-validate-an-entered-text-in-a-kendo-combo-box/
published: true
post_date: 2015-01-13 16:35:02
---
<p>See the plunker for the code: <a title="http://plnkr.co/edit/WroQIwLj4K8vUlVOCkDx?p=preview" href="http://plnkr.co/edit/WroQIwLj4K8vUlVOCkDx?p=preview">http://plnkr.co/edit/WroQIwLj4K8vUlVOCkDx?p=preview</a></p>  <p>&#160;</p>  <p>When no text is entered, the kendo combo box should be invalid:</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/01/image2.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/01/image_thumb2.png" width="414" height="168" /></a></p>  <p>&#160;</p>  <p>When a text is entered, that does not match a valid entry, the kendo combo box should be invalid:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/01/image3.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/01/image_thumb3.png" width="414" height="125" /></a></p>  <p>&#160;</p>  <p>When a text is entered, that does match a valid entry, the kendo combo box should be valid and the selected person should be shown:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/01/image4.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/01/image_thumb4.png" width="437" height="174" /></a></p>
---
ID: 4894
post_title: >
  Kick start unobtrusive validation for
  async loaded content
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2016/05/30/kick-start-unobtrusive-validation-for-async-loaded-content/
published: true
post_date: 2016-05-30 11:14:52
---
<p>&#160;</p>  <p>The jQuery unobtrusive validation was not working for asynchronously loaded html.</p>  <p>We fixed this by kick starting the unobtrusive validation:</p>  <p>&#160;</p>  <p>// Kick start unobtrusive validation for async loaded content   <br />var validator: any = $.validator;    <br />validator.unobtrusive.parse('#PopupForm');</p>
---
ID: 4913
post_title: 'Autofill issues: This is the first time, Chrome disappoints me'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2016/06/08/autofill-issues-this-is-the-first-time-chrome-disappoints-me/
published: true
post_date: 2016-06-08 13:04:25
---
<p>When I set the attribute “autocomplete” to the value “off” on a form element, I expect Chrome, to NOT autofill fields in the form, but that’s not the case.</p>  <p>&#160;</p>  <p>Even if you also add the autocomplete attribute to the input element with value “off”, this is not the case.</p>  <p>&#160;</p>  <p>To get it working I had to add autocomplete=”off” to the form tag and add autocomplete=”new-password” to the &lt;input type=”password” /&gt; field.</p>
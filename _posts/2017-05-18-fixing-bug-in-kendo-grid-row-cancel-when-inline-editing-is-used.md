---
ID: 5072
post_title: >
  Fixing bug in kendo grid row cancel,
  when inline editing is used.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2017/05/18/fixing-bug-in-kendo-grid-row-cancel-when-inline-editing-is-used/
published: true
post_date: 2017-05-18 12:54:26
---
<p><font size="3">I had a strange problem in Kendo grid, when a the last row was canceled the values of the first row were shown in the last row.</font></p>  <p><font size="3">The first fix was adding a cancel even handler:</font></p>    <p><font size="2">cancel: function (e) {     <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; this.cancelChanges();      <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; }</font></p>  <p><font size="3">This fixed the bug, but introduced an other one.</font></p>  <p><font size="3">Now rows would persist the canceled values.</font></p>  <p><font size="3"></font></p>  <p><font size="3">To fix both problem I changed the event handler to:</font></p>  <p><font size="3"></font></p>  <p><font size="2">cancel: function (e) {     <br />&#160;&#160;&#160;&#160;&#160; this.cancelChanges();      <br /> }</font></p>  <p><font size="3"></font></p>  <p><font size="3">I used kendo 2017.1.118</font></p>
---
ID: 448
post_title: 'Get Type of object and get Type of class in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/22/get-type-of-object-and-get-type-of-class-in-c/
published: true
post_date: 2009-05-22 14:49:35
---
<p>Some .NET function require a Type as parameter:</p>  <p><span style="color: green">// To get the Type of an object use:     <br /></span>DummyClass dc = <span style="color: blue">new </span>DummyClass();    <br /><span style="color: #2b91af">Type </span>typeFromObject = dc.GetType();    <br />    <br /><span style="color: green">// To get the Type of an class use:     <br /></span><span style="color: #2b91af">Type </span>typeFromClass = <span style="color: blue">typeof</span>(DummyClass);</p> <a href="http://11011.net/software/vspaste"></a>
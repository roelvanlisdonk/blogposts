---
ID: 513
post_title: >
  Allow nullable parameter on a Microsoft
  ReportingServices Report
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/06/04/allow-nullable-parameter-on-a-microsoft-reportingservices-report/
published: true
post_date: 2009-06-04 20:43:53
---
<p>To allow nullable parameters on a Microsoft Reporting Services report, add an extra row for all product models:    <br /><span style="color: green">     <br />-- Dataset 2       <br /></span><span style="color: blue">select      <br />&#160;&#160;&#160; </span><span style="color: gray">null </span><span style="color: blue">as </span><span style="color: red">'ProductModelID'</span><span style="color: gray">,</span><span style="color: red">'[All models]' </span><span style="color: blue">as </span><span style="color: red">'Name'      <br /></span><span style="color: blue">union select </span>pm<span style="color: gray">.</span>ProductModelID<span style="color: gray">, </span>pm<span style="color: gray">.</span>Name     <br /><span style="color: blue">from      <br />&#160;&#160;&#160; </span>Production<span style="color: gray">.</span>ProductModel pm     <br /><span style="color: blue">order by </span>Name</p> <a href="http://11011.net/software/vspaste"></a>  <br />  <br />  <br />Solution found at: <a title="http://www.discombobulator.net/index.asp?article=9" href="http://www.discombobulator.net/index.asp?article=9">http://www.discombobulator.net/index.asp?article=9</a><a href="http://11011.net/software/vspaste"></a>
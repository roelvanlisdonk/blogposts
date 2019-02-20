---
ID: 925
post_title: 'Xml namespaces in a XDocument with LINQ in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/01/11/xml-namespaces-in-a-xdocument-with-linq-in-c/
published: true
post_date: 2010-01-11 10:55:30
---
<p>If a XML file use namespaces like a Microsoft Excel 2003 XML file, you must use the class XNamespace in you’re LINQ queries for an example see:   <br />    <br /><a title="http://www.roelvanlisdonk.nl/how-to-read-a-microsoft-office-excel-2003-xml-file-with-linq-in-c/" href="http://www.roelvanlisdonk.nl/how-to-read-a-microsoft-office-excel-2003-xml-file-with-linq-in-c/">http://www.roelvanlisdonk.nl/how-to-read-a-microsoft-office-excel-2003-xml-file-with-linq-in-c/</a>    <br />    <br />The Workbook node uses a namespace::</p>  <p>&lt;?xml version=&quot;1.0&quot;?&gt;   <br />&lt;?mso-application progid=&quot;Excel.Sheet&quot;?&gt;    <br />&lt;Workbook xmlns=&quot;urn:schemas-microsoft-com:office:spreadsheet&quot;    <br /> xmlns:o=&quot;urn:schemas-microsoft-com:office:office&quot;    <br /> xmlns:x=&quot;urn:schemas-microsoft-com:office:excel&quot;    <br /> xmlns:ss=&quot;urn:schemas-microsoft-com:office:spreadsheet&quot;    <br /> xmlns:html=&quot;<a href="http://www.w3.org/TR/REC-html40&quot;">http://www.w3.org/TR/REC-html40&quot;</a>&gt;    <br />&lt;/Workbook&gt;</p>
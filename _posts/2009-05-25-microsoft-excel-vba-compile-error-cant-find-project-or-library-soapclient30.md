---
ID: 468
post_title: 'Microsoft Excel &#8211; VBA &#8211; Compile error: Can&#039;t find project or library SoapClient30'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/25/microsoft-excel-vba-compile-error-cant-find-project-or-library-soapclient30/
published: true
post_date: 2009-05-25 11:48:37
---
<p>If you have a VBA macro in Microsoft Excel and a webreference to a webservice, you might get the famous Compile error: Can't find project or library SoapClient30.   <br />In mine case it wasn't missing the C:\Program Files (x86)\Common Files\microsoft shared\OFFICE12\MSSOAP30.DLL but an old reference to the Office 11 components library.    <br />    <br />Solution    <br />&gt; Open the Microsoft visual basic editor    <br />&gt; Tools &gt; References...     <br />&gt; Remove all dll's with &quot;MISSING&quot; for it, if you don't have any start with deleting de selected dll until a dll appears witch is missing.</p>
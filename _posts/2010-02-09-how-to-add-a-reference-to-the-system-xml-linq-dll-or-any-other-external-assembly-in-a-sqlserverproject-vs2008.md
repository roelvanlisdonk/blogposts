---
ID: 1015
post_title: >
  How to add a reference to the
  System.Xml.Linq.dll or any other
  external assembly in a SQLServerProject
  VS2008
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/02/09/how-to-add-a-reference-to-the-system-xml-linq-dll-or-any-other-external-assembly-in-a-sqlserverproject-vs2008/
published: true
post_date: 2010-02-09 13:51:03
---
<p>If you want to add a reference to the System.Xml.Linq.dll in a SQLServerProject VS2008 or any other external assembly just create a normal class library add all you’re references and deploy the created assembly:</p>  <pre class="code"><span style="color: blue">CREATE ASSEMBLY </span>[Rvl.Prototype.CommonClassLibrary.dll]
<span style="color: blue">FROM </span><span style="color: red">'C:\Temp\Rvl.Prototype.CommonClassLibrary.dll'
</span><span style="color: blue">WITH PERMISSION_SET </span><span style="color: gray">= </span><span style="color: blue">UNSAFE
GO</span></pre>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/02/image.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/02/image_thumb.png" width="244" height="153" /></a> </p>

<p>After deploying the normal assembly you can reference that assembly in you’re SqlServerPorject by clicking “Add reference” &gt; SQL Server</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/02/image1.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/02/image_thumb1.png" width="469" height="358" /></a> </p>

<p>Using the “UNSAFE” permmission set might result in errors make sure you’re SQL Server instance has<strong> clr enabled</strong>:</p>

<pre class="code"><span style="color: maroon">sp_configure </span><span style="color: red">'clr enabled'</span><span style="color: gray">, </span>1<span style="color: gray">;
</span><span style="color: blue">GO

RECONFIGURE</span><span style="color: gray">;
</span><span style="color: blue">GO</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>And you’re database property TRUSTWORTHY is ON:</p>

<pre class="code"><span style="color: blue">ALTER DATABASE </span>Mydatabase <span style="color: blue">SET TRUSTWORTHY ON</span><span style="color: gray">;
</span><span style="color: blue">GO</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>The user executing the stored procedure must be sysadmin or you must set correct prermissions, see google.
  </p>
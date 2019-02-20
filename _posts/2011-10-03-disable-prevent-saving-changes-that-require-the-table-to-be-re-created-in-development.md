---
ID: 2159
post_title: 'Disable &quot;prevent saving changes that require the table to be re-created&quot; in development'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/10/03/disable-prevent-saving-changes-that-require-the-table-to-be-re-created-in-development/
published: true
post_date: 2011-10-03 15:13:02
---
<p>By default Microsoft SQL Server Management Studio has the option [Prevent saving changes that require the table to be re-created] enabled. This causes an error, when you want to save changes to a table that require the table to be dropped and re-created.</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/10/image.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/10/image_thumb.png" width="573" height="454" /></a></p>  <p>&#160;</p>  <p>During development you can disable this option: Tools &gt; Options &gt; Designers &gt; Check [Prevent saving changes that require table re-creation]</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/10/image1.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/10/image_thumb1.png" width="580" height="333" /></a></p>
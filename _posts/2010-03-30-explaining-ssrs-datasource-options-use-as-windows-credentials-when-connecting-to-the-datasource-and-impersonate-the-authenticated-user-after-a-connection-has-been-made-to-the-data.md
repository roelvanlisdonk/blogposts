---
ID: 1165
post_title: 'Explaining SSRS datasource options &ldquo;Use as Windows credentials when connecting to the datasource&rdquo; and &ldquo;Impersonate the authenticated user after a connection has been made to the datasource&rdquo;'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/30/explaining-ssrs-datasource-options-use-as-windows-credentials-when-connecting-to-the-datasource-and-impersonate-the-authenticated-user-after-a-connection-has-been-made-to-the-data/
published: true
post_date: 2010-03-30 09:32:46
---
<p>In SSRS ther are two options you can set, when the credentials of the datasource are stored securely in the report server:</p>  <ul>   <li>Use as Windows crendentials when connecting to the datasource</li> </ul>  <blockquote>   <p>This option must be checked, when you want to use “Windows Integrated Security Authentication” and not “SQL Authentication”</p> </blockquote>  <ul>   <li>Impersonate the authenticated user after a connection has been made to the datasource</li> </ul>  <blockquote>   <p>This option must be checked, when you want to use the current user to query the database, instead of the given account. The given account is used to connect to the database, but after the connection has been made, the current user is used to query the database. If the current user does not have permissions an exception will occur.</p> </blockquote>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/03/image29.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/03/image_thumb29.png" width="855" height="784" /></a></p>
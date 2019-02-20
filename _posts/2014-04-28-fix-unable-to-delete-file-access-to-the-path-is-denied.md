---
ID: 3742
post_title: 'Fix: Unable to delete file &quot;&#8230;&quot;. Access to the path &#8216;&#8230;&#8217; is denied.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/04/28/fix-unable-to-delete-file-access-to-the-path-is-denied/
published: true
post_date: 2014-04-28 13:26:44
---
<p>I was getting a build error: “Unable to delete file &quot;...&quot;. Access to the path '...' is denied.”, when building a solution in Microsoft Visual Studio 2013.</p>  <p>I fixed the problem by:</p>  <ul>   <li>Closing Microsoft Visual Studio 2013</li>    <li>Opening a command prompt in administration mode and then, running:</li>    <li>rd /s /q <font color="#a5a5a5">(to remove all file from the debug folder).</font></li> </ul>
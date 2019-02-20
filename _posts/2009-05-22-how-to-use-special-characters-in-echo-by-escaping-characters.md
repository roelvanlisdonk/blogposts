---
ID: 445
post_title: >
  How to use special characters in echo,
  by escaping characters
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/22/how-to-use-special-characters-in-echo-by-escaping-characters/
published: true
post_date: 2009-05-22 14:42:17
---
<p>If you want to use special characters in your echo statement, use the ^ character before the special character. If you want to escape the % character in an echo statement double the % like:    <br />    <br /><strong>Script Test.bat</strong>    <br />echo %%1     <br /><strong>Usage</strong>    <br />C:\Test.bat &#8220;C:\Program Files&#8221;     <br /><strong>Result      <br /></strong>&#8220;C:\Program Files&#8221;     <br />    <br /><strong>Escape character</strong> (<a href="http://www.ss64.com/nt/setlocal.html">http://www.ss64.com/nt/setlocal.html</a>)     <br />Adding the escape character before a command symbol&#160;&#160;&#160;&#160; allows it to be treated as ordinary text.     <br />When piping or redirecting any of these charcters you should     <br />prefix with the escape character: \ &amp; | &gt; &lt; ^     <br />e.g.&#160; ^\&#160; ^&amp;&#160; ^|&#160; ^&gt;&#160; ^&lt;&#160; ^^</p>
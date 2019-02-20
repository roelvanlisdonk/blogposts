---
ID: 4867
post_title: 'Fix: Error CS5001 Program does not contain a static &#8216;Main&#8217; method suitable for an entry point'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2016/05/10/fix-error-cs5001-program-does-not-contain-a-static-main-method-suitable-for-an-entry-point/
published: true
post_date: 2016-05-10 16:52:39
---
<p>&#160;</p>  <p>Starting with version of ASP.NET 5 RC1, the statup.cs must have a static main, see:</p>  <p>&#160;</p>  <p><a title="http://www.talkingdotnet.com/static-void-main-in-asp-net-5-startup-cs/" href="http://www.talkingdotnet.com/static-void-main-in-asp-net-5-startup-cs/">http://www.talkingdotnet.com/static-void-main-in-asp-net-5-startup-cs/</a></p>  <p>&#160;</p>  <p>After I added the main method, the error was fixed.</p>
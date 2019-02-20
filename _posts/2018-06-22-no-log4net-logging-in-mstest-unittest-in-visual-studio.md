---
ID: 5214
post_title: >
  No log4net logging in MSTest UnitTest in
  Visual Studio
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2018/06/22/no-log4net-logging-in-mstest-unittest-in-visual-studio/
published: true
post_date: 2018-06-22 13:34:47
---
<p>
 </p><p>I was testing a C# method that used log4net for logging, when running the code in the production app the method logged to a log file, but when I executed the method inside a UnitTest I wasn't getting any logging.
</p><p>Turns out, I forgot to call <span style="color:black; font-family:Consolas; font-size:9pt"> XmlConfigurator.Configure(); before calling the method.
</span></p>
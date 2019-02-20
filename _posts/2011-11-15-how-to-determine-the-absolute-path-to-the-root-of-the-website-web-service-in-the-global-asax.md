---
ID: 2211
post_title: >
  How to determine the absolute path to
  the root of the website / web service in
  the Global.asax
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/11/15/how-to-determine-the-absolute-path-to-the-root-of-the-website-web-service-in-the-global-asax/
published: true
post_date: 2011-11-15 10:54:21
---
<p>If you want to use the absolute path to the root of the website / web service in the Global.asax you can use the property:</p>  <p>&#160;</p>  <pre class="code">System.Web.<span style="color: #2b91af">HttpRuntime</span>.AppDomainAppPath</pre>
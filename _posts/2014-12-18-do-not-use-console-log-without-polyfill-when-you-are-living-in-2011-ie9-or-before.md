---
ID: 4221
post_title: >
  Do not use console.log without polyfill,
  when you are living in 2011 (IE9) or
  before
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/12/18/do-not-use-console-log-without-polyfill-when-you-are-living-in-2011-ie9-or-before/
published: true
post_date: 2014-12-18 07:34:36
---
<p>If you have to support &lt;= IE9, you should not use console.log without a polyfill. If you don’t use a polyfill, console.log will throw an error. Console.log will only be available if the developertools are open:</p>  <p>&#160;</p>  <p><a title="http://stackoverflow.com/questions/5472938/does-ie9-support-console-log-and-is-it-a-real-function/5473193#5473193" href="http://stackoverflow.com/questions/5472938/does-ie9-support-console-log-and-is-it-a-real-function/5473193#5473193">http://stackoverflow.com/questions/5472938/does-ie9-support-console-log-and-is-it-a-real-function/5473193#5473193</a></p>
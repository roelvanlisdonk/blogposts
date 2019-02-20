---
ID: 243
post_title: Prevent session timeout in ASP .NET 2.0
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/01/31/prevent-session-timeout-in-asp-net-20/
published: true
post_date: 2009-01-31 11:28:14
---
<p>To prevent a session timeout use the meta html tag in the header html tag:</p> <p>&nbsp;</p><pre class="code"><span style="color:blue;">&lt;</span><span style="color:#a31515;">meta </span><span style="color:red;">http-equiv</span><span style="color:blue;">="refresh" </span><span style="color:red;">content</span><span style="color:blue;">="300" /&gt;</span><span style="color:green;">&lt;!-- prevent session timeout --&gt;</span></pre><a href="http://11011.net/software/vspaste"></a>
---
ID: 5120
post_title: Problems with moment.d.ts in v2.18.1
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2017/10/09/problems-with-moment-d-ts-in-v2-18-1/
published: true
post_date: 2017-10-09 13:43:42
---
<p>When you target "es5" in TypeScript and use namespaces instead of import statements, the moment.d.ts delivered with v2.18.1 will not work for you.
</p><p>You must comment the last row in the file: <span style="color:green; font-family:Consolas; font-size:9pt">export = moment;</span>
	</p><p>
 </p>
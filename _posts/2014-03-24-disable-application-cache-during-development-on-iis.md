---
ID: 3694
post_title: >
  Disable Application Cache during
  development on IIS.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/03/24/disable-application-cache-during-development-on-iis/
published: true
post_date: 2014-03-24 14:15:20
---
<p>In production we use Application Cache, to distribute a new version of a Single Page Application. <p>In development I immediately want to see my CSS, JavaScript and HTML code changes, without changing the "*.appcache" on every save. This is why I disable de Application Cache in development by "not serving" the "*.appcache" file:</p><pre class="code">
<span style="background: white; color: blue">&lt;</span><span style="background: white; color: #a31515">system.webServer</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: #a31515">staticContent</span><span style="background: white; color: blue">&gt;
      &lt;</span><span style="background: white; color: #a31515">remove </span><span style="background: white; color: red">fileExtension</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">"</span><span style="background: white; color: blue">.woff</span><span style="background: white; color: black">" </span><span style="background: white; color: blue">/&gt;
      &lt;</span><span style="background: white; color: #a31515">mimeMap </span><span style="background: white; color: red">fileExtension</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">"</span><span style="background: white; color: blue">.woff</span><span style="background: white; color: black">" </span><span style="background: white; color: red">mimeType</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">"</span><span style="background: white; color: blue">application/font-woff</span><span style="background: white; color: black">" </span><span style="background: white; color: blue">/&gt;
      &lt;</span><span style="background: white; color: #a31515">mimeMap </span><span style="background: white; color: red">fileExtension</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">"</span><span style="background: white; color: blue">.appcache</span><span style="background: white; color: black">" </span><span style="background: white; color: red">mimeType</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">"</span><span style="background: white; color: blue">text/cache-manifest</span><span style="background: white; color: black">" </span><span style="background: white; color: blue">/&gt;
      &lt;!-- </span><span style="background: white; color: green">To disable appCache during development, comment line above and uncomment line below. </span><span style="background: white; color: blue">--&gt;
      &lt;!--</span><span style="background: white; color: green">&lt;mimeMap fileExtension=".wrongAppcache" mimeType="text/cache-manifest" /&gt;</span><span style="background: white; color: blue">--&gt;
    &lt;/</span><span style="background: white; color: #a31515">staticContent</span><span style="background: white; color: blue">&gt;

</pre></span>
---
ID: 5227
post_title: 'Fixing &#8211; events.js:183 throw er; // Unhandled &#8216;error&#8217; event, when npm installing PhantomJS'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2018/09/18/fixing-events-js183-throw-er-unhandled-error-event-when-npm-installing-phantomjs/
published: true
post_date: 2018-09-18 11:40:53
---
<p>
 </p><p>When running npm install inside my project folder, I got the error events.js:183 throw er; // Unhandled 'error' event
</p><p>This was caused by an other terminal running my application.
</p><p>After killing al terminals and browsers this error was fixed.
</p><p>
 </p><h1>Error
</h1><p>PS C:\Dev\MyProject1&gt; npm install
</p><p>
 </p><p>&gt; entry@0.0.0 postinstall C:\Dev\MyProject1
</p><p>&gt; webdriver-manager update &amp; node node_modules/phantomjs-prebuilt/install.js
</p><p>
 </p><p>events.js:183
</p><p>      throw er; // Unhandled 'error' event
</p><p>      ^
</p><p>
 </p><p>Error: read ECONNRESET
</p><p>    at TLSWrap.onread (net.js:622:25)
</p><p>Found PhantomJS at C:\Dev\MyProject1\node_modules\phantomjs-prebuilt\lib\phantom\bin\phantomjs.exe ...verifying
</p><p>PhantomJS is previously installed at C:\Dev\\MyProject1\node_modules\phantomjs-prebuilt\lib\phantom\bin\phantomjs.exe</p>
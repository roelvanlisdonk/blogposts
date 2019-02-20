---
ID: 3226
post_title: >
  How to automatically remove phonegap.js
  (cordova.js) from GitHub before build by
  phonegap build service.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/05/31/how-to-automatically-remove-phonegap-js-cordova-js-from-github-before-build-by-phonegap-build-service/
published: true
post_date: 2013-05-31 16:00:38
---
<p>If you want to use the PhoneGap Build service, you must remove the phonegap.js (cordova.js) from your source files, because PhoneGap requires a different phonegap.js JavaScript file for each platform and using an incompatible phonegap.js will result in errors when running your application.</p>  <p>&#160;</p>  <p>For this I use the .gitignore file (<a href="https://help.github.com/articles/ignoring-files">https://help.github.com/articles/ignoring-files</a>), so the phonegap.js is never pushed to the GitHub repository, but it can be used during development on the localmachine.</p>
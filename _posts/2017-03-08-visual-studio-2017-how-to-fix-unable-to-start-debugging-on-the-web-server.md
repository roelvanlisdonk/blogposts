---
ID: 5065
post_title: 'Visual Studio 2017 &#8211; How to fix: Unable to start debugging on the web server.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2017/03/08/visual-studio-2017-how-to-fix-unable-to-start-debugging-on-the-web-server/
published: true
post_date: 2017-03-08 09:43:43
---
<p>When I first started Visual Studio 2017 after a clean installation I got the error:</p>  <p>Unable to start debugging on the web server. IIS does not list a web site that matches the launched URL.</p>    <p>When debugging a new asp.net project.</p>    <p>Turns out I was not running Visual Studio 2017 as Administrator.</p>    <p>To fix this see:</p>  <p><a title="https://olivierpaes.wordpress.com/2016/06/26/unable-to-start-debugging-on-the-web-server-iis-does-not-list-a-web-site-that-matches-the-launched-url/" href="https://olivierpaes.wordpress.com/2016/06/26/unable-to-start-debugging-on-the-web-server-iis-does-not-list-a-web-site-that-matches-the-launched-url/">https://olivierpaes.wordpress.com/2016/06/26/unable-to-start-debugging-on-the-web-server-iis-does-not-list-a-web-site-that-matches-the-launched-url/</a></p>  <p>or</p>  <p><a title="http://stackoverflow.com/questions/10716956/iis-does-not-list-a-website-that-matches-the-launch-url" href="http://stackoverflow.com/questions/10716956/iis-does-not-list-a-website-that-matches-the-launch-url">http://stackoverflow.com/questions/10716956/iis-does-not-list-a-website-that-matches-the-launch-url</a></p>
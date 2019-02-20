---
ID: 5053
post_title: 'Fix in IE &#8211; Angular 1.6.1 Disabling automatic bootstrap. &lt;script&gt; protocol indicates an extension, document.location.href does not match.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2017/02/01/fix-in-ie-angular-1-6-1-disabling-automatic-bootstrap-script-protocol-indicates-an-extension-document-location-href-does-not-match/
published: true
post_date: 2017-02-01 09:56:38
---
<pre>
<p>When using angular 1.6.1 in IE9, IE10, IE11, I was getting the error:
</p><p><br /></p><p><strong>Disabling automatic bootstrap. &lt;script&gt; protocol indicates an extension, </strong></p><p><strong>document.location.href does not match.</strong></p><p><br /></p><p>
</p><p>This seemed to be an 1.5.x issue, that was fixed in 1.5.11, but I was getting the error in 1.6.1.
</p><p>To fix the error I switched from automatic bootstrapping (ng-app) to manual bootstrapping.
</p><p>So I changed: &lt;html xmlns:ng=&quot;<a href="http://angularjs.org&quot;">http://angularjs.org&quot;</a> id=&quot;ng-app&quot; ng-app=”myapp&quot;&gt;
</p><p>to: &lt;html&gt; </p>

<p>And after my module declaration:</p>
<p>angular.module('myapp', []);</p><p>angular.element(document).ready(function () {  <br />    angular.bootstrap(document, ['myapp']);<br />});</p>
</pre>
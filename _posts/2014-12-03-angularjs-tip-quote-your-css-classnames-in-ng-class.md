---
ID: 4177
post_title: >
  AngularJS tip, quote your css classnames
  in ng-class
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/12/03/angularjs-tip-quote-your-css-classnames-in-ng-class/
published: true
post_date: 2014-12-03 10:07:53
---
<p>It is a common practice to use spinalcase in CSS, like the css class “<strong>.ada-wizard-marker”.</strong></p>  <p>If you want to use this class in a ng-class directive, where the input is an object, use single quotes, like:</p>  <pre class="code"><span style="background: white; color: red">ng-class</span><span style="background: white; color: blue">=&quot;{ 'ada-wizard-marker': vm.showToolTip }&quot;</span></pre>


<p>If you don’t use the single quotes, ng-class will not work.</p>
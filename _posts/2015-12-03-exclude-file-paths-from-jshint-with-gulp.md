---
ID: 4689
post_title: Exclude file paths from jshint with gulp
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/12/03/exclude-file-paths-from-jshint-with-gulp/
published: true
post_date: 2015-12-03 08:51:14
---
<p>If you want to jshint all JavaScript files in a folder, but want to exclude a subfolder, you can use “negation” in gulp.</p>  <p>&#160;</p>  <p>&#160;</p>  <p>var gulp = require(&quot;gulp&quot;);</p>  <p>var jshint = require(&quot;gulp-jshint&quot;);   <br />var plumber = require(&quot;gulp-plumber&quot;);</p>  <p>&#160;</p>  <p>var onError = function (err) {   <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; console.log(err);    <br />&#160;&#160;&#160; };    <br /></p>  <p>/**   <br />&#160;&#160;&#160;&#160; * Hint all of our custom developed Javascript files.    <br />&#160;&#160;&#160;&#160; */    <br />&#160;&#160;&#160; gulp.task(&quot;jshint&quot;, function () {</p>  <p>&#160;&#160;&#160;&#160;&#160;&#160;&#160; return gulp.src([   <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &quot;Client/**/*.js&quot;,    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <font color="#ff0000"> &quot;!Client/Libraries/**/*.js&quot;     <br /></font>&#160;&#160;&#160;&#160;&#160;&#160;&#160; ])    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; .pipe(plumber({    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; errorHandler: onError    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; }))    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; .pipe(jshint())    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; .pipe(jshint.reporter(&quot;default&quot;));    <br />&#160;&#160;&#160; });</p>
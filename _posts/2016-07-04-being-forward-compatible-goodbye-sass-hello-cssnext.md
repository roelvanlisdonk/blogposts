---
ID: 4932
post_title: 'Being forward compatible &#8211; Goodbye SASS hello CSSNext'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2016/07/04/being-forward-compatible-goodbye-sass-hello-cssnext/
published: true
post_date: 2016-07-04 13:58:36
---
<span style="color: #333333; font-family: Helvetica; font-size: 10pt;">Instead of being backwards compatible we want to be forward compatible.
</span>

<span style="color: #333333; font-family: Helvetica; font-size: 10pt;">But what do I mean with "forward compatible"?
</span>

<span style="color: #333333; font-family: Helvetica; font-size: 10pt;">Well that's when we write our code against the next standard spec, but compile down to older specs to be backwards compatible, so for example:
</span>

&nbsp;

<span style="color: #333333; font-family: Times New Roman; font-size: 18pt;">TypeScript
</span>

&nbsp;

<span style="color: #333333; font-family: Helvetica; font-size: 10pt;">We use TypeScript to write modern ES6, ES7, ES8 code, but we compile down to ES5 to be backwards compatible with older browsers.
</span>

&nbsp;

<span style="color: #333333; font-family: Times New Roman; font-size: 18pt;">CSSNext
</span>

&nbsp;

<span style="color: #333333; font-family: Helvetica; font-size: 10pt;">The only reason we used SASS in the current project, was to re-use color variables in css.
</span>

<span style="color: #333333; font-family: Helvetica; font-size: 10pt;">Now the css next spec includes custom properties (variables), so to be forward compatible we decided to port our SASS to CSSNext.
</span>

&nbsp;

<span style="color: #333333; font-family: Times New Roman; font-size: 18pt;">CSSNext with PostCSS</span>

&nbsp;

PostCSS is a node package that can be installed by using NPM, it can be used to pre-process CSS by using JavaScript / TypeScript.

One of the many plugins of PostCSS is een CSSNext plugin, in the following example I will be using this plugin to convert CSSNext code into normal CSS3 code.

<span style="color: #333333; font-family: Helvetica; font-size: 10pt;">In this example I will be using Visual Studio 2015 update 3.
</span>

&nbsp;

&nbsp;
<h3>Create a new MVC web project</h3>
&nbsp;

<span style="color: #333333; font-family: Helvetica; font-size: 10pt;">File &gt; New &gt; Project...
Installed &gt; Templates &gt; Visual C# &gt; Web &gt; ASP.NET Web Application (.NET Framework) &gt; MVC
</span>

&nbsp;
<h3>Add a package.json file to the root of the web application</h3>
&nbsp;

<span style="color: black; font-family: Courier New; font-size: 9pt;">{
</span>

<span style="color: black; font-family: Courier New; font-size: 9pt;"><span style="color: #2e75b6;">"dependencies"<span style="color: black;">: {</span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: #2e75b6;">"angular"<span style="color: black;">: <span style="color: #a31515;">"1.2.29"<span style="color: black;">,</span></span></span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: #2e75b6;">"es5-shim"<span style="color: black;">: <span style="color: #a31515;">"&gt;=4.5.9"<span style="color: black;">,</span></span></span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: #2e75b6;">"es6-shim"<span style="color: black;">: <span style="color: #a31515;">"&gt;=0.35.1"<span style="color: black;">,</span></span></span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: #2e75b6;">"spin.js"<span style="color: black;">: <span style="color: #a31515;">"&gt;=2.3.2"<span style="color: black;">
</span></span></span></span></span>

<span style="color: black; font-family: Courier New; font-size: 9pt;"> },</span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: #2e75b6;">"devDependencies"<span style="color: black;">: {</span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: #2e75b6;">"del"<span style="color: black;">: <span style="color: #a31515;">"&gt;=2.2.1"<span style="color: black;">,</span></span></span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: #2e75b6;">"gulp"<span style="color: black;">: <span style="color: #a31515;">"&gt;=3.9.1"<span style="color: black;">,</span></span></span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: #2e75b6;">"gulp-debug"<span style="color: black;">: <span style="color: #a31515;">"&gt;=2.1.2"<span style="color: black;">,</span></span></span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: #2e75b6;">"gulp-postcss"<span style="color: black;">: <span style="color: #a31515;">"&gt;=6.1.1"<span style="color: black;">,</span></span></span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: #2e75b6;">"gulp-rename"<span style="color: black;">: <span style="color: #a31515;">"&gt;=1.2.2"<span style="color: black;">,</span></span></span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: #2e75b6;">"gulp-util"<span style="color: black;">: <span style="color: #a31515;">"&gt;=3.0.7"<span style="color: black;">,</span></span></span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: #2e75b6;">"postcss-import"<span style="color: black;">: <span style="color: #a31515;">"&gt;=8.1.2"<span style="color: black;">,</span></span></span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: #2e75b6;">"postcss-cssnext"<span style="color: black;">: <span style="color: #a31515;">"&gt;=2.7.0"<span style="color: black;">
</span></span></span></span></span>

<span style="color: black; font-family: Courier New; font-size: 9pt;"> },</span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: #2e75b6;">"name"<span style="color: black;">: <span style="color: #a31515;">"WebApplication1"<span style="color: black;">,</span></span></span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: #2e75b6;">"private"<span style="color: black;">: <span style="color: blue;">true<span style="color: black;">,</span></span></span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: #2e75b6;">"scripts"<span style="color: black;">: {</span></span></span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: #2e75b6;">"gulp"<span style="color: black;">: <span style="color: #a31515;">"gulp"<span style="color: black;">
</span></span></span></span></span>

<span style="color: black; font-family: Courier New; font-size: 9pt;"> },</span><span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: #2e75b6;">"version"<span style="color: black;">: <span style="color: #a31515;">"1.0.1"<span style="color: black;">
</span></span></span></span></span>

<span style="font-family: Courier New;"><span style="color: black; font-size: 9pt;">}</span>
</span>

&nbsp;
<h3>Add a gulpfile.js to the root of the web application</h3>
&nbsp;

<span style="color: green; font-family: Courier New; font-size: 9pt;">/**
</span>

<span style="color: green; font-family: Courier New; font-size: 9pt;"> * The version of gulp and all it's dependencies are managed in the package.json file.
</span>

<span style="color: green; font-family: Courier New; font-size: 9pt;"> */<span style="color: black;">
</span></span>

<span style="color: #a31515; font-family: Courier New; font-size: 9pt;">'use strict'<span style="color: black;">;
</span></span>

<span style="color: green; font-family: Courier New; font-size: 9pt;">// Dependencies<span style="color: black;">
</span></span>

<span style="color: blue; font-family: Courier New; font-size: 9pt;">const<span style="color: black;"> gulp = require(<span style="color: #a31515;">'gulp'<span style="color: black;">);
</span></span></span></span>

<span style="color: blue; font-family: Courier New; font-size: 9pt;">const<span style="color: black;"> postcss = require(<span style="color: #a31515;">'gulp-postcss'<span style="color: black;">);
</span></span></span></span>

<span style="color: blue; font-family: Courier New; font-size: 9pt;">const<span style="color: black;"> postcssImport = require(<span style="color: #a31515;">'postcss-import'<span style="color: black;">);
</span></span></span></span>

<span style="color: blue; font-family: Courier New; font-size: 9pt;">const<span style="color: black;"> postcssNext = require(<span style="color: #a31515;">'postcss-cssnext'<span style="color: black;">);
</span></span></span></span>

<span style="color: blue; font-family: Courier New; font-size: 9pt;">const<span style="color: black;"> rename = require(<span style="color: #a31515;">'gulp-rename'<span style="color: black;">);
</span></span></span></span>

<span style="color: blue; font-family: Courier New; font-size: 9pt;">const<span style="color: black;"> defaultTheme = <span style="color: #a31515;">'Stigas'<span style="color: black;">;
</span></span></span></span>

<span style="color: green; font-family: Courier New; font-size: 9pt;">/**
</span>

<span style="color: green; font-family: Courier New; font-size: 9pt;"> * The default task.
</span>

<span style="color: green; font-family: Courier New; font-size: 9pt;"> */<span style="color: black;">
</span></span>

<span style="color: black; font-family: Courier New; font-size: 9pt;">gulp.task(<span style="color: #a31515;">'default'<span style="color: black;">, <span style="color: blue;">function<span style="color: black;"> () {
</span></span></span></span></span>

<span style="color: black; font-family: Courier New; font-size: 9pt;">});
</span>

<span style="color: black; font-family: Courier New; font-size: 9pt;">gulp.task(<span style="color: #a31515;">'apply-theming'<span style="color: black;">, <span style="color: blue;">function<span style="color: black;"> () {
</span></span></span></span></span>

<span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: blue;">var<span style="color: black;"> plugins = [
</span></span></span>

<span style="color: black; font-family: Courier New; font-size: 9pt;"> postcssImport,
</span>

<span style="color: black; font-family: Courier New; font-size: 9pt;"> postcssNext
</span>

<span style="color: black; font-family: Courier New; font-size: 9pt;"> ];
</span>

<span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: blue;">return<span style="color: black;"> gulp.src(<span style="color: #a31515;">'./Content/Site.cssnext'<span style="color: black;">)
</span></span></span></span></span>

<span style="color: black; font-family: Courier New; font-size: 9pt;"> .pipe(postcss(plugins))
</span>

<span style="color: black; font-family: Courier New; font-size: 9pt;"> .pipe(rename({
</span>

<span style="color: black; font-family: Courier New; font-size: 9pt;"> extname: <span style="color: #a31515;">".css"<span style="color: black;">
</span></span></span>

<span style="color: black; font-family: Courier New; font-size: 9pt;"> }))
</span>

<span style="color: black; font-family: Courier New; font-size: 9pt;"> .pipe(gulp.dest(<span style="color: #a31515;">'./Content'<span style="color: black;">));
</span></span></span>

<span style="color: black; font-family: Courier New;"><span style="font-size: 9pt;">});</span><span style="color: #333333; font-size: 10pt;">
</span></span>
<h3>Add a "Content/variables.cssnext" file</h3>
&nbsp;

<span style="color: maroon; font-family: Courier New; font-size: 9pt;">:root<span style="color: black;"> {
</span></span>

<span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: red;">--mainColor<span style="color: black;">: <span style="color: blue;">rgb(255, 0, 0)<span style="color: black;">;
</span></span></span></span></span>

<span style="color: black; font-family: Courier New;"><span style="font-size: 9pt;">}</span><span style="color: #333333; font-size: 10pt;">
</span></span>

&nbsp;
<h3>Rename the existing Site.css to Site.cssnext</h3>
&nbsp;

<span style="color: #333333;"><span style="font-family: Helvetica; font-size: 10pt;">At the following text at the top of the Site.cssnext file: </span><span style="color: purple;"><span style="font-family: Courier New; font-size: 9pt;">@import<span style="color: black;">
<span style="color: blue;">"./variables.cssnext"<span style="color: black;">;</span></span></span></span><span style="color: #333333; font-family: Helvetica; font-size: 10pt;">
</span></span></span>

<span style="color: #333333; font-family: Helvetica; font-size: 10pt;">And at the following css rule at the end of this script:
</span>

<span style="color: maroon; font-family: Courier New; font-size: 9pt;">p<span style="color: black;"> {
</span></span>

<span style="color: black; font-family: Courier New; font-size: 9pt;">
<span style="color: red;">color<span style="color: black;">: <span style="color: blue;">var(--mainColor)<span style="color: black;">;
</span></span></span></span></span>

<span style="color: black; font-family: Courier New;"><span style="font-size: 9pt;">}</span><span style="color: #333333; font-size: 10pt;">
</span></span>

<span style="color: #333333; font-family: Helvetica; font-size: 10pt;">Now run the gulp task "apply-theming" by using the Task Runner Explorer or on the command line: </span><strong>npm run gulp -- apply-theming</strong><span style="color: #333333; font-family: Helvetica; font-size: 10pt;">
</span>

&nbsp;

<img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/07/070416_1201_Beingforwar1-1.png" alt="" /><span style="color: #333333; font-family: Helvetica; font-size: 10pt;">
</span>

&nbsp;

&nbsp;

<span style="color: #333333; font-family: Helvetica; font-size: 10pt;">Now when you run the web application you should see the text in red:
</span>

<img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/07/070416_1201_Beingforwar2-1.png" alt="" /><span style="color: #333333; font-family: Helvetica; font-size: 10pt;">
</span>

&nbsp;

&nbsp;

<span style="color: #333333; font-family: Helvetica; font-size: 10pt;">
</span>
---
ID: 4296
post_title: >
  Getting started with gulp and livereload
  in Visual Studio 15
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/03/19/getting-started-with-gulp-and-livereload-in-visual-studio-15/
published: true
post_date: 2015-03-19 09:30:48
---
<p>If you want to automatically refresh your web page, when a file on disk changes you can use gulp and the gulp plugin: gulp-livereload.</p>  <p>&#160;</p>  <p><strong>Notes</strong></p>  <ul>   <li>Microsoft Visual Studio 2015 has <strong>node</strong> included out of the box, for Microsoft Visual Studio 2013, you will have to manually install node.</li>    <li>Microsoft Visual Studio 2015 has the <strong>task runner explorer</strong> included out of the box, for Microsoft Visual Studio 2013, you will have to manually install this as a Visual Studio extension.</li> </ul>  <p>&#160;</p>  <p><strong>Command prompt</strong></p>  <ul>   <li>Open cmd (with administrator rights)</li>    <li>Change directory to folder containing the web project, e.g. cd &quot;C:\..\..\MySolution\MyProjectWeb&quot;</li> </ul>  <p><strong>Install gulp globally</strong></p>  <ul>   <li>npm install gulp --g</li> </ul>  <p><strong>Install gulp to project</strong></p>  <ul>   <li>npm install gulp --save-dev</li> </ul>  <p><strong>Install gulp plugins</strong></p>  <ul>   <li>npm install gulp-jshint --save-dev</li>    <li>npm install gulp-notify --save-dev</li>    <li>npm install gulp-plumber --save-dev</li>    <li>npm install gulp-watch --save-dev</li>    <li>npm install gulp-livereload --save-dev</li> </ul>  <p><strong>Add gulpfile.js to project</strong></p>  <ul>   <li>Add a gulpfile.js to the root of the visual studio project</li>    <li>Add code to the gulpfile:</li> </ul>  <p><strong>gulpfile.js contents</strong></p>  <pre class="code"><span style="background: white; color: blue">var </span><span style="background: white; color: black">gulp = require(</span><span style="background: white; color: #a31515">'gulp'</span><span style="background: white; color: black">);
</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">jshint = require(</span><span style="background: white; color: #a31515">'gulp-jshint'</span><span style="background: white; color: black">);
</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">plumber = require(</span><span style="background: white; color: #a31515">'gulp-plumber'</span><span style="background: white; color: black">);
</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">livereload = require(</span><span style="background: white; color: #a31515">'gulp-livereload'</span><span style="background: white; color: black">);

</span><span style="background: white; color: green">// Gulp plumber error handler
</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">onError = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(err) {
    console.log(err);
};

gulp.task(</span><span style="background: white; color: #a31515">'reload'</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
    </span><span style="background: white; color: green">// Change the filepath, when you want to live reload a different page in your project.
    </span><span style="background: white; color: black">livereload.reload(</span><span style="background: white; color: #a31515">&quot;./index.html&quot;</span><span style="background: white; color: black">);
});

</span><span style="background: white; color: green">// This task should be run, when you want to reload the webpage, when files change on disk.
// This task will only watch JavaScript file changes in the folder &quot;/Client&quot; and it's subfolders.
</span><span style="background: white; color: black">gulp.task(</span><span style="background: white; color: #a31515">'watch'</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
    livereload.listen();
    gulp.watch(</span><span style="background: white; color: #a31515">'./Client/**/*.js'</span><span style="background: white; color: black">, [</span><span style="background: white; color: #a31515">'reload'</span><span style="background: white; color: black">]);
});

</span><span style="background: white; color: green">// Hint all of our custom developed Javascript to make sure things are clean.
// This task will only hint JavaScript files in the folder &quot;/Client&quot; and it's subfolders.
</span><span style="background: white; color: black">gulp.task(</span><span style="background: white; color: #a31515">'jshint'</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
    </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">gulp.src([
        </span><span style="background: white; color: #a31515">'./Client/**/*.js'
    </span><span style="background: white; color: black">])
    .pipe(plumber({
        errorHandler: onError
    }))
    .pipe(jshint())
    .pipe(jshint.reporter(</span><span style="background: white; color: #a31515">'default'</span><span style="background: white; color: black">));
});

</span><span style="background: white; color: green">// When the user enters &quot;gulp&quot; on the command line, the default task will automatically be called.
// This default task below, will run all other task automatically.
// So when the user enters &quot;gulp&quot; on the command line all task are run.
</span><span style="background: white; color: black">gulp.task(</span><span style="background: white; color: #a31515">'default'</span><span style="background: white; color: black">, [</span><span style="background: white; color: #a31515">'jshint'</span><span style="background: white; color: black">]);</span></pre>

<p>&#160;</p>

<p><strong>Run the gulp task “watch” with the Task Runner Explorer</strong></p>

<p>This task will watch, the file system for any JavaScript file changes and call the “reload” gulp task, when this occurs.</p>

<p>The “reload” gulp task will tell the browser to refresh itself.</p>

<p>&#160;</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/03/image4.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/03/image_thumb4.png" width="580" height="239" /></a></p>

<p>&#160;</p>

<p>&#160;</p>

<p><strong>Install LiveReload chrome extension</strong></p>

<p><a title="https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei" href="https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei">https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei</a></p>

<p>&#160;</p>

<p><strong>Start debugging your website from Visual Studio in Chrome and enable the LiveReload chrome extension</strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/03/image5.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/03/image_thumb5.png" width="580" height="100" /></a></p>

<p>&#160;</p>

<p>&#160;</p>

<p><strong>Make as change</strong></p>

<p>Make a change to a JavaScript file and see the changes live reflected in your browser.</p>
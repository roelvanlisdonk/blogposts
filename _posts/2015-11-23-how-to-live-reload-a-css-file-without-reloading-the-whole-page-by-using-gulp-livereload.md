---
ID: 4675
post_title: >
  How to live reload a css file, without
  reloading the whole page, by using
  gulp-livereload.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/11/23/how-to-live-reload-a-css-file-without-reloading-the-whole-page-by-using-gulp-livereload/
published: true
post_date: 2015-11-23 14:58:14
---
<p>&#160;</p>  <p>If you want to only reload css and not the entire page, when files change on disk, you can use the following gulp file.</p>  <p>&#160;</p>  <pre class="code"><p><span style="background: white; color: green">/**
 * When you want to use this gulpfile.js, make sure you execute the gulp.ps1 PowerShell script first, so everything is installed correctly.
 */
</span><span style="background: white; color: black">(</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(require) {
    </span><span style="background: white; color: #a31515">&quot;use strict&quot;</span><span style="background: white; color: black">;

</span><span style="background: white; color: green">    // Gulp.
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">gulp = require(</span><span style="background: white; color: #a31515">&quot;gulp&quot;</span><span style="background: white; color: black">);

    </span><span style="background: white; color: green">// Gulp plugins.</span><span style="background: white; color: black">
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">plumber = require(</span><span style="background: white; color: #a31515">&quot;gulp-plumber&quot;</span><span style="background: white; color: black">);
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">livereload = require(</span><span style="background: white; color: #a31515">&quot;gulp-livereload&quot;</span><span style="background: white; color: black">);
    </span></p><p><span style="background: white; color: black">    </span><span style="background: white; color: green">// Gulp plumber error handler
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">onError = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(err) {
        console.log(err);
    };

    </span><span style="background: white; color: green">/**
     * The following file will be reloaded, when one of the &quot;watched&quot; *.html or 8.js files has changed.
     */
    </span><span style="background: white; color: black">gulp.task(</span><span style="background: white; color: #a31515">'reload'</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
        gulp.src([</span><span style="background: white; color: green">
            </span><span style="background: white; color: #a31515">&quot;App/unit.test.runner.html&quot;
        </span><span style="background: white; color: black">])
        .on(</span><span style="background: white; color: #a31515">'error'</span><span style="background: white; color: black">, onError)
        .pipe(gulp.dest(</span><span style="background: white; color: #a31515">'dist'</span><span style="background: white; color: black">))
        .pipe(livereload());
    });

    </span><span style="background: white; color: green">/**
     * All *.css files will be reloaded, when one of the &quot;watched&quot; *.css files has changed.
     */
    </span><span style="background: white; color: black">gulp.task(</span><span style="background: white; color: #a31515">'reloadCss'</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
        gulp.src([
            </span><span style="background: white; color: #a31515">'App/**/*.css'
        </span><span style="background: white; color: black">])
        .on(</span><span style="background: white; color: #a31515">'error'</span><span style="background: white; color: black">, onError)
        .pipe(gulp.dest(</span><span style="background: white; color: #a31515">'dist'</span><span style="background: white; color: black">))
        .pipe(livereload());
    });

    </span><span style="background: white; color: green">/**
        Watch *.css files, but only reload css, not the entire page.
        Watch *.html and *.js files, when a change is detected, reload the whole page.
    */
    </span><span style="background: white; color: black">gulp.task(</span><span style="background: white; color: #a31515">&quot;watch&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
        livereload.listen();

        gulp.watch([
            </span><span style="background: white; color: #a31515">&quot;App/**/*.css&quot;
        </span><span style="background: white; color: black">], [</span><span style="background: white; color: #a31515">&quot;reloadCss&quot;</span><span style="background: white; color: black">]);

        gulp.watch([
            </span><span style="background: white; color: #a31515">&quot;App/**/*.html&quot;</span><span style="background: white; color: black">,
            </span><span style="background: white; color: #a31515">&quot;App/**/*.js&quot;
        </span><span style="background: white; color: black">], [</span><span style="background: white; color: #a31515">&quot;reload&quot;</span><span style="background: white; color: black">]);
    });
        
    </span><span style="background: white; color: green">/**
        When the user enters &quot;gulp&quot; on the command line, the default task will automatically be called.
        This default task below, will run all other task automatically.
        So when the user enters &quot;gulp&quot; on the command line all task are run.
     */
    </span><span style="background: white; color: black">gulp.task(</span><span style="background: white; color: #a31515">&quot;default&quot;</span><span style="background: white; color: black">, [</span><span style="background: white; color: #a31515">&quot;watch&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;reload&quot;</span><span style="background: white; color: black">]);

}(require));
</span></p></pre>
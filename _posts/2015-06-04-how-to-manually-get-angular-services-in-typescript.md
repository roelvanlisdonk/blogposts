---
ID: 4376
post_title: >
  How to manually get Angular services in
  TypeScript
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/06/04/how-to-manually-get-angular-services-in-typescript/
published: true
post_date: 2015-06-04 12:58:41
---
<p>If you manually want to get / use Angular services in TypeScript you can use the following code:</p>  <p>&#160;</p>  <pre class="code"><span style="background: white; color: green">/// &lt;reference path=&quot;../libraries/angular/angular.d.ts&quot; /&gt;

</span><span style="background: white; color: blue">module </span><span style="background: white; color: black">app {
    </span><span style="background: white; color: #a31515">&quot;use strict&quot;</span><span style="background: white; color: black">;

    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">appModule = angular.module(</span><span style="background: white; color: #a31515">&quot;app&quot;</span><span style="background: white; color: black">, []);
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">injector: angular.auto.IInjectorService = angular.injector([</span><span style="background: white; color: #a31515">&quot;ng&quot;</span><span style="background: white; color: black">]);
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">httpService: angular.IHttpService = injector.get(</span><span style="background: white; color: #a31515">&quot;$http&quot;</span><span style="background: white; color: black">);
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">qService: angular.IQService = injector.get(</span><span style="background: white; color: #a31515">&quot;$q&quot;</span><span style="background: white; color: black">);
}</span></pre>
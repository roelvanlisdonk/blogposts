---
ID: 4904
post_title: 'Fix: Visual Studio doesn&rsquo;t use or can&rsquo;t find TypeScript typings (*.d.ts) in a .net core project'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2016/06/03/fix-visual-studio-doesnt-use-or-cant-find-typescript-typings-d-ts-in-a-net-core-project/
published: true
post_date: 2016-06-03 13:03:58
---
<p>&#160;</p>  <p>I added some TypeScripts typings to a .net core project in Visual Studio 2015&#160; (version 14.0.25123.00 Update 2), by using the NPM package “typings”, but the added *.d.ts files, were not picked up by Visual Studio, this was caused by excluding the “wwwroot” folder in the tsconfig.json, </p>  <p>&#160;</p>  <p>after removing the wwwroot folder from the exclude array, the typings were correctly found and used.</p>  <p>&#160;</p>  <p>&#160;</p>  <p>&#160;</p>  <p>{   <br />&#160; &quot;compileOnSave&quot;: true,    <br />&#160; &quot;compilerOptions&quot;: {    <br />&#160;&#160;&#160; &quot;module&quot;: &quot;system&quot;,    <br />&#160;&#160;&#160; &quot;noImplicitAny&quot;: false,    <br />&#160;&#160;&#160; &quot;noEmitOnError&quot;: true,    <br />&#160;&#160;&#160; &quot;removeComments&quot;: false,    <br />&#160;&#160;&#160; &quot;sourceMap&quot;: true,    <br />&#160;&#160;&#160; &quot;target&quot;: &quot;es6&quot;    <br />&#160; },    <br />&#160; &quot;exclude&quot;: [    <br />&#160;&#160;&#160; &quot;node_modules&quot;,</p>  <p>&#160;&#160;&#160;&#160; &quot;wwwroot&quot; &lt;========================= Remove the wwwroot   <br />&#160; ]    <br />}</p>
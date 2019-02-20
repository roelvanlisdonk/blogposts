---
ID: 4982
post_title: 'Fixing: NPM / Node error on Windows: The specified path, file name, or both are too long. The fully qualified file name must be less than 260 characters, and the directory name must be less than 248 characters.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2016/09/07/fixing-npm-node-error-on-windows-the-specified-path-file-name-or-both-are-too-long-the-fully-qualified-file-name-must-be-less-than-260-characters-and-the-directory-name-must-be-less-than-248-c/
published: true
post_date: 2016-09-07 09:10:17
---
<p>I was using Visual Studio 2015 update 3 on Windows 10 x64 and was getting the error: “The specified path, file name, or both are too long. The fully qualified file name must be less than 260 characters, and the directory name must be less than 248 characters.”, when running some gulp tasks.</p>  <br />  <p>I fixed the problem by letting Visual Studio 2015 update 3 use the “current”(at the time of writing) node version (v6.5.0), that was&#160; installed in “C:\Program Files\nodejs”.</p>  <br />  <br />  <p><strong>Steps</strong></p>  <ul>   <li>Download the “current” (v6.5.0) Windows x64 version of node (NOT, I repeat, NOT the LTS version) at <a title="https://nodejs.org/en/" href="https://nodejs.org/en/">https://nodejs.org/en/</a></li>    <li>Install it</li>    <li>Open Visual Studio 2015 &gt; Tools &gt; Options… &gt; Project and Solutions &gt; External Web Tools &gt; Add an entry “C:\Program Files\nodejs”</li>    <li>Move the entry to the top of the list and restart visual studio:</li> </ul>  <br />  <br />  <p><a href="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/09/image.png" rel="lightbox"><img title="image" style="display: inline; background-image: none;" border="0" alt="image" src="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/09/image_thumb.png" width="735" height="430" /></a></p>  <br />  <br />  <br />  <p>No the following steps might not be necessary, but in case the error persists:</p>  <ul>   <li>Remove the node_modules folder</li>    <li>Open the solution and project (this will trigger an npm install)</li>    <li>Open the Package Manger Console</li>    <li>npm cache clean</li>    <li>npm dedupe</li>    <li>npm install</li> </ul>
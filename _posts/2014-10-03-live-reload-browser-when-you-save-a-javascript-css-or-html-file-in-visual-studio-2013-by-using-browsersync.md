---
ID: 4050
post_title: >
  Live reload browser, when you save a
  JavaScript, CSS or HTML file in Visual
  Studio 2013, by using BrowserSync or
  BrowserLink
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/10/03/live-reload-browser-when-you-save-a-javascript-css-or-html-file-in-visual-studio-2013-by-using-browsersync/
published: true
post_date: 2014-10-03 08:28:50
---
<p>&#160;</p>  <p>If you want to speed up your SPA development process, it would be nice if you could reload all browser currently showing your SPA, when you press CTRL-S in Visual Studio 2013. The build-in Browserlink provides this feature for ASP .NET WebForms en ASP .NET MVC, but you could also use BrowserSync, which will work with any editor.</p>  <p>&#160;</p>  <p><strong>BrowserSync</strong></p>  <p>&#160;</p>  <p>1. Download node.js <a title="http://nodejs.org/download/" href="http://nodejs.org/download/">http://nodejs.org/download/</a></p>  <p>2. Install node.js (next – next – finish)</p>  <p>3. Open a command prompt (with administrator privileges) and enter:</p>  <p>4. npm install -g browser-sync</p>  <p>5. Change directory to the location of your Visual Studio solution file:</p>  <p>&#160;&#160;&#160; - CD “C:\Projects\MyProject”</p>  <p>5. Start your web application in Visual Studio by pressing F5</p>  <p>&#160;&#160;&#160; - Look at the browser address bar to get the URL to connect BrowserSync to, in my case localhost:50367</p>  <p>6. To start watching all files in all subfolders, at the command prompt enter:</p>  <p>&#160;&#160;&#160; browser-sync start --proxy &quot;localhost:50367&quot; --files &quot;**.*&quot;</p>  <p>&#160;</p>  <p>This will start a new instance of the default browser on an other port, showing your site connected to BrowserSync</p>  <p>In my case the new url was: <a title="http://localhost:3000/ " href="http://localhost:3000/ ">http://localhost:3000/ </a></p>  <p>Now when you edit a file in Visual Studio en press CTRL-S the browser at <a href="http://localhost:3000">http://localhost:3000</a> will be refreshed.</p>  <p>&#160;</p>  <p><strong>BrowserLink</strong></p>  <p>BrowserLink is provided in the box with Microsoft Visual Studio 2013, but OOB it will not work with SPA applications created with only html, JavaScript and CSS files.</p>  <p>To get BrowserLink working with those kind of web applications add the following to the web.config: </p>  <pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: #a31515">system.webServer</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: #a31515">handlers</span><span style="background: white; color: blue">&gt;
      </span><span style="background: white; color: blue">      &lt;</span><span style="background: white; color: #a31515">add </span><span style="background: white; color: red">name</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">Browser Link for HTML</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">path</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">*.html</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">verb</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">*</span><span style="background: white; color: black">&quot;
           </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">System.Web.StaticFileHandler, System.Web, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</span><span style="background: white; color: black">&quot;
           </span><span style="background: white; color: red">resourceType</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">File</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">preCondition</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">integratedMode</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: blue">/&gt;
    &lt;/</span><span style="background: white; color: #a31515">handlers</span><span style="background: white; color: blue">&gt;
  &lt;/</span><span style="background: white; color: #a31515">system.webServer</span><span style="background: white; color: blue">&gt;</span></pre>


<p>The good thing about BrowserLink that it is in the box and you don’t have to specify all subfolders you want to watch.</p>

<p>The downside is that you still have to use CTRL-S and CTRL-ALT-ENTER. This can be an upside if you want to edit multiple files en then refresh the connected browsers.</p>

<p>For now I will stick with BrowserLink, because it’s in the box.</p>

<p>&#160;</p>

<p>Note: when using the “empty” asp .net template, I could not get BrowserLink to work, but when I used the web api template all was just fine.</p>
---
ID: 4767
post_title: >
  Starting with ASP .NET 5 (empty project)
  and static files.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2016/01/15/starting-with-asp-net-empty-project-and-static-files/
published: true
post_date: 2016-01-15 13:43:21
---
&nbsp;

If you are starting with ASP .NET 5 (1.0.0-rc1-final) and you just want to serve an “index.html”, you can follow these steps:
<ul>
	<li>Start Visual Studio 2015</li>
	<li>File &gt; New &gt; Project…</li>
	<li>Installed &gt; Templates &gt; Visual C# &gt; Web &gt; ASP.NET Web Application</li>
	<li>Choose .NET Framework 4.6.1</li>
</ul>
<a href="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/01/image-3.png" rel="lightbox"><img style="background-image: none; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-width: 0px;" title="image" src="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/01/image_thumb-3.png" alt="image" width="580" height="405" border="0" /></a>

&nbsp;
<ul>
	<li>ASP.NET 5 Templates &gt; Empty</li>
</ul>
<a href="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/01/image-4.png" rel="lightbox"><img style="background-image: none; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-width: 0px;" title="image" src="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/01/image_thumb-4.png" alt="image" width="580" height="453" border="0" /></a>

&nbsp;
<ul>
	<li>Open project.json and add package dependency "Microsoft.AspNet.StaticFiles": "1.0.0-rc1-final":</li>
</ul>
&nbsp;

<a href="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/01/image-5.png" rel="lightbox"><img style="background-image: none; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-width: 0px;" title="image" src="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/01/image_thumb-5.png" alt="image" width="580" height="518" border="0" /></a>

&nbsp;
<ul>
	<li>Open Startup.cs and remove the app.Run lines:</li>
</ul>
<a href="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/01/image-6.png" rel="lightbox"><img style="background-image: none; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-width: 0px;" title="image" src="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/01/image_thumb-6.png" alt="image" width="580" height="520" border="0" /></a>

&nbsp;
<ul>
	<li>In Startup.cs add the follwoing lines in the Configure methode beneath app.UseIISPlatformHandler();:
<ul>
	<li>app.UseDefaultFiles();</li>
	<li>app.UseStaticFiles();</li>
</ul>
</li>
	<li>Like so:</li>
</ul>
<a href="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/01/image-7.png" rel="lightbox"><img style="background-image: none; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-width: 0px;" title="image" src="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/01/image_thumb-7.png" alt="image" width="704" height="456" border="0" /></a>

&nbsp;

&nbsp;
<ul>
	<li>Add an index.html file to the wwwroot folder and add the text “Hello world from html” to the body:</li>
</ul>
&nbsp;

<a href="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/01/image-8.png" rel="lightbox"><img style="background-image: none; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-width: 0px;" title="image" src="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/01/image_thumb-8.png" alt="image" width="580" height="518" border="0" /></a>

&nbsp;

&nbsp;

&nbsp;

Press F5 and the a browser should appear showing you the “Hello world from html”

&nbsp;

<a href="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/01/image-9.png" rel="lightbox"><img style="background-image: none; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-width: 0px;" title="image" src="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/01/image_thumb-9.png" alt="image" width="579" height="652" border="0" /></a>
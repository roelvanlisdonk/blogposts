---
ID: 5136
post_title: 'Allow *.css, *.js and *.html from the MVC 5 Views map'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2017/11/10/allow-css-js-and-html-from-the-mvc-5-views-map/
published: true
post_date: 2017-11-10 14:20:07
---
<p>
 </p><p>If you want to allow static content to be served from the asp .net MVC 5 views folder, just added the web.config in this folder and change path="*" to path="*.cshtml".
</p><p>https://stackoverflow.com/questions/17949460/how-do-you-request-static-html-files-under-the-views-folder-in-asp-net-mvc
</p><p>
 </p><p><span style="color:blue; font-family:Consolas; font-size:9pt">  &lt;<span style="color:#a31515">system.webServer<span style="color:blue">&gt;<span style="color:black">
					</span></span></span></span></p><p><span style="color:blue; font-family:Consolas; font-size:9pt">    &lt;<span style="color:#a31515">handlers<span style="color:blue">&gt;<span style="color:black">
					</span></span></span></span></p><p><span style="color:blue; font-family:Consolas; font-size:9pt">      &lt;<span style="color:#a31515">remove<span style="color:blue">
					<span style="color:red">name<span style="color:blue">=<span style="color:black">"<span style="color:blue">BlockViewHandler<span style="color:black">"<span style="color:blue">/&gt;<span style="color:black">
											</span></span></span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Consolas; font-size:9pt">      &lt;<span style="color:#a31515">add<span style="color:blue">
					<span style="color:red">name<span style="color:blue">=<span style="color:black">"<span style="color:blue">BlockViewHandler<span style="color:black">"<span style="color:blue">
											<span style="color:red">path<span style="color:blue">=<span style="color:black">"<span style="color:blue">*.cshtml<span style="color:black">"<span style="color:blue">
																	<span style="color:red">verb<span style="color:blue">=<span style="color:black">"<span style="color:blue">*<span style="color:black">"<span style="color:blue">
																							<span style="color:red">preCondition<span style="color:blue">=<span style="color:black">"<span style="color:blue">integratedMode<span style="color:black">"<span style="color:blue">
																													<span style="color:red">type<span style="color:blue">=<span style="color:black">"<span style="color:blue">System.Web.HttpNotFoundHandler<span style="color:black">"<span style="color:blue"> /&gt;<span style="color:black">
																																			</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Consolas; font-size:9pt">    &lt;/<span style="color:#a31515">handlers<span style="color:blue">&gt;<span style="color:black">
					</span></span></span></span></p><p><span style="color:blue; font-family:Consolas; font-size:9pt">  &lt;/<span style="color:#a31515">system.webServer<span style="color:blue">&gt;</span></span></span></p>
---
ID: 2322
post_title: 'Solving: HttpContext.Current.User.Identity.Name is empty, when using Windows Authentication.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/12/28/solving-httpcontext-current-user-identity-name-is-empty-when-using-windows-authentication/
published: true
post_date: 2011-12-28 11:02:22
---
<p>If you want to use Windows Authentication in your ASP .NET website, you need to add the &lt;authentication mode=&quot;Windows&quot;/&gt; tag in the Web.config. </p>  <pre class="code"><span style="color: blue">&lt;</span><span style="color: #a31515">system.web</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">authentication </span><span style="color: red">mode</span><span style="color: blue">=</span>&quot;<span style="color: blue">Windows</span>&quot;<span style="color: blue">/&gt;
</span></pre>


<p>If the HttpContext.Current.user.Identity.Name is still empty. Check the authentication feature of the web application in IIS, make sure all authentication mechanisms are Disabled, except for the Windows Authentication, this should be set to Enabled.</p>

<p>&#160;</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/12/image14.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/12/image_thumb14.png" width="87" height="106" /></a></p>

<p>&#160;</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/12/image15.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/12/image_thumb15.png" width="435" height="239" /></a></p>
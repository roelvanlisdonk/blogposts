---
ID: 3582
post_title: 'How to set / overwrite the Context.User.IsInRole for debugging/testing purposes in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/11/20/how-to-set-overwrite-the-context-user-isinrole-for-debuggingtesting-purposes-in-c/
published: true
post_date: 2013-11-20 09:16:47
---
<p>In my case I wanted to debug a ASP .NET MVC application, that used Windows authentication, but my account was not added to the &quot;Administrators&quot; role in development. If you still want to debug the site as an Administrator you can set the role of the authenticated user in the Global.asax.</p>  <pre class="code"><span style="background: white; color: blue">protected void </span><span style="background: white; color: black">Application_AuthenticateRequest(</span><span style="background: white; color: #2b91af">Object </span><span style="background: white; color: black">sender, </span><span style="background: white; color: #2b91af">EventArgs </span><span style="background: white; color: black">e)
{
    </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(Context.User != </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">)
    {
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">userPrincipal = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">GenericPrincipal</span><span style="background: white; color: black">(Context.User.Identity, </span><span style="background: white; color: blue">new string</span><span style="background: white; color: black">[] { </span><span style="background: white; color: #a31515">&quot;Adminstrators&quot; </span><span style="background: white; color: black">});
        Context.User = userPrincipal;
    } 
}</span></pre>
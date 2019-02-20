---
ID: 3130
post_title: 'Fix: Forms authentication timeout after 20 minutes, even if timeout is set to 1440 minutes'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/01/02/fix-forms-authentication-timeout-after-20-minutes-even-if-timeout-is-set-to-1440-minutes/
published: true
post_date: 2013-01-02 13:11:18
---
<p>If you are using ASP .NET with forms authentication and set the forms authentication to 1440 minutes, this authentication will by default expire after 20 minutes, when the server gets no request during these 20 minutes. This is controlled by the application pool setting [<strong>Idle Time-out (minutes)</strong>]:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/01/image.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/01/image_thumb.png" width="327" height="396" /></a></p>  <p>&#160;</p>  <p>Settings this value to 1440 and setting the forms authentication timeout in the web.config to 1440, solved my problem.</p>  <pre>&lt;authentication mode=&quot;Forms&quot;&gt;
    &lt;forms loginUrl=&quot;~/Account/Login.aspx&quot; <strong>timeout=&quot;1440&quot;</strong> protection=&quot;All&quot; defaultUrl=&quot;Default.aspx&quot;/&gt;
&lt;/authentication&gt;</pre>

<p>Found my solution in one of the comments on:</p>

<p><a title="http://www.codeproject.com/Questions/163203/Forms-Authentication-and-or-Session-timeout" href="http://www.codeproject.com/Questions/163203/Forms-Authentication-and-or-Session-timeout">http://www.codeproject.com/Questions/163203/Forms-Authentication-and-or-Session-timeout</a></p>

<p>&#160;</p>

<p><strong>Notes</strong></p>

<ul>
  <li>
    <div align="left">Changes to application pool settings are stored in the applicationhost.config file, stored at C:\Windows\System32\inetsrv\config\applicationHost.config</div>
  </li>
</ul>
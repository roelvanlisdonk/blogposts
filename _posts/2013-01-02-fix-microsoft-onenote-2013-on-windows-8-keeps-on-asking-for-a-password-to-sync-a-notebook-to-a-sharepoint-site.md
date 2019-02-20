---
ID: 3134
post_title: 'Fix: Microsoft OneNote 2013 on Windows 8 keeps on asking for a password to sync a notebook to a SharePoint site.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/01/02/fix-microsoft-onenote-2013-on-windows-8-keeps-on-asking-for-a-password-to-sync-a-notebook-to-a-sharepoint-site/
published: true
post_date: 2013-01-02 14:50:41
---
<p>Microsoft OneNote 2013 on Windows 8 kept on asking for a password to sync a notebook to a local SharePoint site.</p>  <p>This was caused by a Windows 2008 domain controller not pushing domain policy settings to a Windows 8 client.</p>  <p>The Windows 8 client didn’t have the SharePoint site added to the local intranet zone.</p>  <p>&#160;</p>  <p>To fix this problem I had to manually add the <a href="http://*.mydomain.com">http://*.mydomain.com</a> and <a href="https://*.mydomain.com">https://*.mydomain.com</a> to the local intranet zone:</p>  <p>&#160;</p>  <p>Control panel &gt; Internet Options &gt; tab:Security &gt; Local Intranet &gt; Sites &gt; Advanced</p>  <p>Uncheck &quot;Automatically detect intranet network&quot; and add your intranet sites:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/02/image4.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/02/image_thumb4.png" width="580" height="424" /></a></p>
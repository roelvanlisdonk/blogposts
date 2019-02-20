---
ID: 453
post_title: >
  Renaming a Microsoft Office Sharepoint
  Server or WSS server
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/22/renaming-a-microsoft-office-sharepoint-server-or-wss-server/
published: true
post_date: 2009-05-22 14:58:12
---
<p>When you want to rename you&#8217;re MOSS or WSS Server follow the steps on the following site:    <br /><a href="http://www.sharepointblogs.com/mirjam/archive/2007/08/06/renaming-a-moss-server.aspx">http://www.sharepointblogs.com/mirjam/archive/2007/08/06/renaming-a-moss-server.aspx</a>    <br />But if you&#8217;re like me and renamed you&#8217;re server before you red that blog post. You&#8217;re SharePoint 3.0 Central Administration link will not work, DNS errors.     <br />In mine case it was because I had some old alternate access mappings with the old servername in it,     <br />but I could not change the mappings, because I could not get the Central Administration page loaded, without DNS errors.     <br />    <br />To solve this problem I edited the HOST file in C:\Windows\System32\drivers\etc and added 127.0.0.1&#160;&#160;&#160; &lt;OLDSERVERNAME&gt;     <br />After a ipconfig /flushdns and ipconfig /registerdns the central administration page was accesible.     <br />After changing the alternate access mappings to the new server name, the original HOST file could be restored </p>
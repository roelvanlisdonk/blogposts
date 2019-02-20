---
ID: 1459
post_title: 'Stop the presses: mega performance boost for Microsoft SharePoint 2010 on opening office documents, by using a Internet Explorer setting'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/06/16/stop-the-presses-mega-performance-boost-for-microsoft-sharepoint-2010-on-opening-office-documents-by-using-a-internet-explorer-setting/
published: true
post_date: 2010-06-16 08:44:56
---
We are using Microsoft SharePoint for our intranet since 2006, but users started to put there office documents local or on other products like TFS, NAS (File Share), just because opening a Microsoft Office document would take a lot of time (ranging from 10s to 2 minutes). The VISIO documents were the worst of all (always waiting for minutes before I could start working on the document, but then when I saved the Microsoft VISIO document I was waiting for minutes again).  So after being frustrated for over 4 years, here comes along our Microsoft SharePoint Administrator: <strong>Jan Willem Nieuwenhuizen</strong>, he did a google on it and found the solution:

Start Internet Explorer &gt; Tools &gt; Internet Options &gt; Connections &gt; LAN settings":

Disable “Automatically detect settings”

Enable “Use a proxy server for LAN (These settings will not apply to dial-up or VPN connections)”

Enable “Bypass proxy server for local addresses”

&nbsp;

<a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/06/image15.png"><img style="display: inline; border: 0px;" title="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/06/image_thumb15.png" border="0" alt="image" width="504" height="442" /></a>

Press Advanced

<a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/06/image14.png"><img style="display: inline; border: 0px;" title="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/06/image_thumb14.png" border="0" alt="image" width="504" height="540" /></a>

Enter *.* in the “Do not use proxy server for addresses beginning with”:

Press OK

Can I have a hooray for JW: hooray hooray hooray
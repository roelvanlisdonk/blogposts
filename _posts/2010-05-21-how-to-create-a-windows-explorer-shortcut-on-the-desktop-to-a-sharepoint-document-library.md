---
ID: 1423
post_title: >
  How to create a windows explorer
  shortcut on the desktop to a SharePoint
  document library
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/05/21/how-to-create-a-windows-explorer-shortcut-on-the-desktop-to-a-sharepoint-document-library/
published: true
post_date: 2010-05-21 11:16:16
---
<p align="left">If you want to create a shortcut on you’re desktop to a SharePoint document library, follow the steps on: <a title="http://www.endusersharepoint.com/2008/02/13/endusersharepointcom-update-on-creating-a-desktop-shortcut-to-a-sharepoint-library/" href="http://www.endusersharepoint.com/2008/02/13/endusersharepointcom-update-on-creating-a-desktop-shortcut-to-a-sharepoint-library/">http://www.endusersharepoint.com/2008/02/13/endusersharepointcom-update-on-creating-a-desktop-shortcut-to-a-sharepoint-library/</a></p>  <p align="left">&#160;</p>  <p align="left">This will create a shortcut with a target formated like: <font color="#800000">&quot;\\<strong>MySharePointSite.MyDomain.nl</strong>\<strong>DavWWWRoot</strong>\Site1\SubSite1\Shared Documents&quot;</font></p>  <ul>   <li>     <div align="left">MySharePointSite.MyDomain.nl = Top-level site collection hostheader</div>   </li>    <li>     <div align="left">DavWWWRoot = Indicates the URL should be opened in the Windows Explorer and not Internet Explorer</div>   </li>    <li>     <div align="left">Site1 = First site beneath the top site collection</div>   </li>    <li>     <div align="left">SubSite1 = First site beneath Site1</div>   </li>    <li>     <div align="left">Shared Documents = Document library name</div>   </li> </ul>  <p align="left">Remember: Pasting the internet URL (<a href="http://MySharePointSite.MyDomain.nl/Site1/SubSite1/Shared%20Documents">http://MySharePointSite.MyDomain.nl/Site1/SubSite1/Shared%20Documents</a>) directly in the <strong>Windows</strong> Explorer will open <strong>Internet</strong> Explorer, so you can use the internet URL to open the document library directly in Windows Explorer, you must use the <font color="#800000"><a href="file://\\MySharePointSite.MyDomain.nl\DavWWWRoot\Site1\SubSite1\Shared&nbsp;Documents">\\<strong>MySharePointSite.MyDomain.nl</strong>\<strong>DavWWWRoot</strong>\Site1\SubSite1\Shared Documents</a></font> format</p>  <p align="left">&#160;</p>  <p align="left"><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/05/image69.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/05/image_thumb68.png" width="304" height="625" /></a></p>
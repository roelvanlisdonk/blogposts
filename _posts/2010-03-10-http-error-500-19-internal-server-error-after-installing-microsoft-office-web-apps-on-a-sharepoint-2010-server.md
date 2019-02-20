---
ID: 1084
post_title: 'HTTP Error 500.19 &ndash; Internal Server Error after installing Microsoft Office Web Apps on a SharePoint 2010 Server'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/10/http-error-500-19-internal-server-error-after-installing-microsoft-office-web-apps-on-a-sharepoint-2010-server/
published: true
post_date: 2010-03-10 08:14:35
---
<p>After installing Microsoft Office Web Apps (following the steps on <a title="http://technet.microsoft.com/en-us/library/ff431687(office.14).aspx#bkmk_ins_exis_sa" href="http://technet.microsoft.com/en-us/library/ff431687(office.14).aspx#bkmk_ins_exis_sa">http://technet.microsoft.com/en-us/library/ff431687(office.14).aspx#bkmk_ins_exis_sa</a>) on a Microsoft SharePoint 2010 server, I got a HTTP Error 500.19 when accessing the SharePiont Sites.</p>  <p>&#160;</p>  <p><strong>Error</strong></p>  <p>Config section 'system.webServer/staticContent' already defined. Sections must only appear once per config file. See the help topic &lt;location&gt; for exceptions </p>  <p>490:&#160;&#160;&#160;&#160; &lt;/staticContent&gt;   <br /> 491:&#160;&#160;&#160;&#160; &lt;staticContent /&gt;    <br /> 492:&#160;&#160; &lt;/system.webServer</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/03/image6.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/03/image_thumb6.png" width="604" height="391" /></a> </p>  <p>&#160;</p>  <p>After removing the double &lt;staticContent /&gt; the site started working again.   </p>
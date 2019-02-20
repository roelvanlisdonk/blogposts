---
ID: 370
post_title: Stop all MOSS 2007 services
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/11/stop-all-moss-2007-services/
published: true
post_date: 2009-05-11 13:32:46
---
<p>To stop all Microsoft Sharepoint Services 2007 - Windows Services, create a bat file and enter the following lines:</p> <p>net stop "SPTimerV3"<br />net stop "SPAdmin"<br />net stop "SPTrace"<br />net stop "SQLWriter"<br />net stop "OSearch"</p>
---
ID: 356
post_title: >
  The report server has encountered a
  configuration error.
  (rsServerConfigurationError)
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/04/17/the-report-server-has-encountered-a-configuration-error-rsserverconfigurationerror/
published: true
post_date: 2009-04-17 12:09:19
---
<p>After installing a second Microsoft Reporting Services instance, I encountered the following error:<br /><br /><a href="http://roelvanlisdonk.files.wordpress.com/2009/04/image2.png"><img style="border-bottom:0;border-left:0;border-top:0;border-right:0;" border="0" alt="image" src="http://roelvanlisdonk.files.wordpress.com/2009/04/image-thumb2.png" width="545" height="410"></a> <br /><br /><strong>Cause and Solution</strong><br />The first Microsoft Reporting Services instance used a sharepoint integrated mode database and the second Microsoft Reporting Services instance used that database.<br />Creating a new database for the second instance in "Native" mode solved the problem.</p>
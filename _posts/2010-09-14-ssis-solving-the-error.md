---
ID: 1719
post_title: 'SSIS Solving: Error loading &#8216;TestPackage 7.database&#8217; : Deserialization failed: The method or operation is not implemented.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/09/14/ssis-solving-the-error/
published: true
post_date: 2010-09-14 12:46:45
---
<p>I was working on an old SSIS project in Microsoft SQL Server Business Intelligence Development Studio 2005 and when I opened a package I got the error:</p>  <p>Error loading 'TestPackage 7.database' : Deserialization failed: The method or operation is not implemented.</p>  <p><strong>Solution</strong></p>  <p>The folder containing the project file <strong>MyProject.dtproj</strong>, should contain only one *.database file, named exactly like the project name, like <strong>MyProject.database</strong>, remove all other *.database files and make sure, you’re versioning system does not contain any *.database files, exclude them from you’re versioning system.</p>
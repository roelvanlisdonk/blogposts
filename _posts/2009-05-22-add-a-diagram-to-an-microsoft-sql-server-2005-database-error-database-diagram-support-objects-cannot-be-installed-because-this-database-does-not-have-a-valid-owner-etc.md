---
ID: 415
post_title: 'Add a diagram to an Microsoft SQL Server 2005 database, Error: Database diagram support objects cannot be installed because this database does not have a valid owner etc.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/22/add-a-diagram-to-an-microsoft-sql-server-2005-database-error-database-diagram-support-objects-cannot-be-installed-because-this-database-does-not-have-a-valid-owner-etc/
published: true
post_date: 2009-05-22 07:54:09
---
<p>When trying to add a diagram to an SQL Server 2005 db I got the following error:   <br />Database diagram support objects cannot be installed because this database does not have a valid owner.     <br />To continue, first use the Files page of the Database Properties dialog box or the ALTER AUTHORIZATION statement     <br />to set the database owner to a valid login, then add the database diagram support objects.    <br />In SQL Server Management Studio do the following:    <br />Right Click on your database, choose properties     <br />Goto the Options Page     <br />In the Dropdown at right labeled &quot;Compatibility Level&quot; choose &quot;SQL Server 2005(90)&quot;    <br />    <br /><a href="http://forums.microsoft.com/MSDN/ShowPost.aspx?PostID=228352&amp;SiteID=1">http://forums.microsoft.com/MSDN/ShowPost.aspx?PostID=228352&amp;SiteID=1</a></p>
---
ID: 2771
post_title: >
  Fix / restore user and login mappings in
  SQL Server
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/07/17/fix-restore-user-and-login-mappings-in-sql-server/
published: true
post_date: 2012-07-17 10:43:42
---
<p>If you restore a SQL Server (&lt; 2012) database on an other database server make sure you fix the user and login mappings by following the steps on <a href="http://atakala.com/browser/Item.aspx?user_id=amos&amp;dict_id=2036">http://atakala.com/browser/Item.aspx?user_id=amos&amp;dict_id=2036</a></p>  <p><strong>Short fix:</strong></p>  <p>use MyDatabase</p>  <p>go</p>  <p>sp_change_users_login 'update_one', 'myusername', 'myloginname'</p>  <p align="left">&#160;</p>  <p align="left"><strong>Note</strong></p>  <p align="left">On SQL Server 2012 you can use <strong>Contained Databases</strong>, see <a href="http://blog.master-it.nl/blog00224/SQL_Server_2012_Contained_Databases_geen_Orphaned_Users_meer.htm">http://blog.master-it.nl/blog00224/SQL_Server_2012_Contained_Databases_geen_Orphaned_Users_meer.htm</a></p>
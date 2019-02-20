---
ID: 455
post_title: >
  To select all sql database roles in a
  database query the sysusers table not
  the sysroles table
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/22/to-select-all-sql-database-roles-in-a-database-query-the-sysusers-table-not-the-sysroles-table/
published: true
post_date: 2009-05-22 15:06:40
---
<p>To select all sql database roles query the systusers table and not the sysroles table, because it does not exist. All roles are stored in the sysusers table    <br />select * from dbo.sysusers where issqlrole = 1</p>
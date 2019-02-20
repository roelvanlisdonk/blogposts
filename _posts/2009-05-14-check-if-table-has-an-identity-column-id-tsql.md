---
ID: 376
post_title: 'Check if table has an identity column &quot;id&quot; &#8211; TSQL'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/14/check-if-table-has-an-identity-column-id-tsql/
published: true
post_date: 2009-05-14 06:25:21
---
<p>declare @tablename varchar(100) <p>set @tablename = 'Product' <p>if exists (select 1 from sys.columns sc inner join sys.objects so on so.Object_Id = sc.Object_Id where&nbsp; sc.name = 'Id' and sc.is_identity = 1 and so.Type = 'U' and so.Name = @tablename) <p>begin <p>&nbsp; print 'Table has an identity column named id' <p>end<br /><br />This can be used to determine if the reseed function can be called on a table.</p>
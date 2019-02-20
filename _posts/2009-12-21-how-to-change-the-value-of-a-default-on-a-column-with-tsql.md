---
ID: 867
post_title: >
  How to change the value of a default on
  a column with TSQL
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/12/21/how-to-change-the-value-of-a-default-on-a-column-with-tsql/
published: true
post_date: 2009-12-21 11:43:33
---
If you want to change the value of default on a column, you must use the ALTER TABLE syntax (DROP DEFAULT and CREATE DEFAULT should be avoided, will be removed in future releases):
<pre class="code"><span style="color: green;">-- Create a default on column 'cust_name' in table 'MyCustomer' with value 'new customer'
</span><span style="color: blue;">IF </span><span style="color: magenta;">OBJECT_ID</span><span style="color: gray;">(</span><span style="color: red;">'dbo.MyCustomers'</span><span style="color: gray;">) IS NOT NULL
  </span><span style="color: blue;">DROP TABLE </span>dbo<span style="color: gray;">.</span>MyCustomers
<span style="color: blue;">go
CREATE TABLE </span>dbo<span style="color: gray;">.</span>MyCustomers<span style="color: gray;">(
  </span>cust_id <span style="color: blue;">int </span><span style="color: gray;">NOT NULL,
  </span>cust_name <span style="color: blue;">varchar</span><span style="color: gray;">(</span>30<span style="color: gray;">) NOT NULL </span><span style="color: blue;">DEFAULT </span><span style="color: gray;">(</span><span style="color: red;">'new customer'</span><span style="color: gray;">))

</span><span>-- Remove the default from column 'MyColumn1' in table 'MyTable'
declare @defaultName varchar(100), @cmd varchar(1000)
set @defaultName =
(
 select name
 from sys.objects so JOIN sys.sysconstraints sc on so.object_id = sc.constid
 where object_name(so.parent_object_id) = 'MyTable'
 and so.type = 'D'
 and sc.colid = (select column_id from sys.columns where name = 'MyColumn1' and Object_ID = Object_ID(N'MyTable'))
)
set @cmd = 'alter table MyTable drop constraint ' + @defaultName
exec(@cmd)</span>
<span style="color: green;">
-- Add a default on column 'cust_name' in table 'MyCustomer' with value 'new text customer'
</span><span style="color: blue;">alter table </span>MyCustomers <span style="color: blue;">add constraint </span>DF_MyCustomers_cust_name <span style="color: blue;">default </span><span style="color: red;">'new text customer' </span><span style="color: blue;">for </span>cust_name<span style="color: gray;">;</span></pre>
<a href="http://11011.net/software/vspaste"></a>
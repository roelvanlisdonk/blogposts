---
ID: 4323
post_title: >
  How to add multiple constraints to one
  column, when creating a table with T-SQL
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/05/04/how-to-add-multiple-constraints-to-one-column-when-creating-a-table-with-t-sql/
published: true
post_date: 2015-05-04 14:36:41
---
<p>&#160;</p>  <p>If you want to add a “named” default and a “named” unique constraint to one column, when creating a table with T-SQL, you can use the “inline syntax”:</p>  <p>&#160;</p>  <p>Here we create a table with a column “Code”, that has a “named” default and a “named” unique constraint:</p>  <pre class="code"><span style="color: blue">if </span><span style="color: magenta">object_id</span><span style="color: gray">(</span><span style="color: red">'dbo.Product'</span><span style="color: gray">) is null
</span><span style="color: blue">begin
    create table </span>dbo<span style="color: gray">.</span>Product
    <span style="color: gray">(
        </span>Id <span style="color: blue">int identity</span><span style="color: gray">(</span>1<span style="color: gray">,</span>1<span style="color: gray">) not null </span><span style="color: blue">constraint </span>PK_dbo_Product_Id <span style="color: blue">primary key</span><span style="color: gray">,
        </span>Code <span style="color: blue">uniqueidentifier </span><span style="color: gray">not null </span><span style="color: blue">constraint </span>UQ_dbo_Product_Code <span style="color: blue">unique</span><span style="color: gray">(</span>Code<span style="color: gray">)
                                       </span><span style="color: blue">constraint </span>DF_dbo_Product_Code <span style="color: blue">default </span><span style="color: magenta">newid</span><span style="color: gray">()
    )
</span><span style="color: blue">end
go
</span></pre>
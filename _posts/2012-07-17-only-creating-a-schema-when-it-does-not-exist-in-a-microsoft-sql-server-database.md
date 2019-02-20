---
ID: 2773
post_title: >
  Only creating a schema, when it does not
  exist in a Microsoft SQL Server
  database.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/07/17/only-creating-a-schema-when-it-does-not-exist-in-a-microsoft-sql-server-database/
published: true
post_date: 2012-07-17 13:51:48
---
<p>If you want to create a schema in a Microsoft SQL Server database only when it does not exist, use:</p>  <pre class="code"><span style="color: blue">declare </span><span style="color: teal">@SchemaName </span><span style="color: blue">nvarchar</span><span style="color: gray">(</span>128<span style="color: gray">)
</span><span style="color: blue">set </span><span style="color: teal">@SchemaName </span><span style="color: gray">= </span><span style="color: red">'Staging'

</span><span style="color: blue">if </span><span style="color: gray">not exists(</span><span style="color: blue">select top </span>1 1 <span style="color: blue">from </span><span style="color: green">information_schema</span><span style="color: gray">.</span><span style="color: green">schemata </span><span style="color: blue">where </span><span style="color: magenta">schema_name </span><span style="color: gray">= </span><span style="color: teal">@SchemaName</span><span style="color: gray">)
</span><span style="color: blue">begin
    exec</span><span style="color: gray">(</span><span style="color: red">'create schema ' </span><span style="color: gray">+ </span><span style="color: teal">@SchemaName</span><span style="color: gray">)
</span><span style="color: blue">end
go
</span></pre>
---
ID: 2906
post_title: >
  How to drop a foreign key based on a
  table name and column name with T-SQL.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/10/23/how-to-drop-a-foreign-key-based-on-a-table-name-and-column-name-with-t-sql/
published: true
post_date: 2012-10-23 14:55:57
---
<p>If you want to delete a foreign key based on a given table name and column name in T-SQL, you can use the following code snippet:</p>  <p>Full table name = [MySchema1].[MyTable1]</p>  <p>Full column name = [MyColumn1]</p>  <pre class="code"><span style="background: white; color: blue">declare </span><span style="background: white; color: black">@TableName </span><span style="background: white; color: blue">varchar</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">255</span><span style="background: white; color: gray">)
</span><span style="background: white; color: blue">set </span><span style="background: white; color: black">@TableName </span><span style="background: white; color: gray">= </span><span style="background: white; color: red">'[MySchema1].[MyTable1]'

</span><span style="background: white; color: blue">declare </span><span style="background: white; color: black">@ColumnName </span><span style="background: white; color: blue">varchar</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">255</span><span style="background: white; color: gray">)
</span><span style="background: white; color: blue">set </span><span style="background: white; color: black">@ColumnName </span><span style="background: white; color: gray">= </span><span style="background: white; color: red">'MyColumn1'

</span><span style="background: white; color: blue">declare </span><span style="background: white; color: black">@TabelObjectId </span><span style="background: white; color: blue">int
set </span><span style="background: white; color: black">@tabelObjectId </span><span style="background: white; color: gray">= </span><span style="background: white; color: magenta">Object_ID</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">@TableName</span><span style="background: white; color: gray">)

</span><span style="background: white; color: blue">declare </span><span style="background: white; color: black">@ForeignKeyObjectId </span><span style="background: white; color: blue">int
select        </span><span style="background: white; color: black">@ForeignKeyObjectId </span><span style="background: white; color: gray">= </span><span style="background: white; color: black">fc</span><span style="background: white; color: gray">.</span><span style="background: white; color: black">constraint_object_id
</span><span style="background: white; color: blue">from        </span><span style="background: white; color: green">sys</span><span style="background: white; color: gray">.</span><span style="background: white; color: green">foreign_key_columns </span><span style="background: white; color: black">fc
</span><span style="background: white; color: gray">inner join    </span><span style="background: white; color: green">sys</span><span style="background: white; color: gray">.</span><span style="background: white; color: green">columns </span><span style="background: white; color: black">c  </span><span style="background: white; color: blue">on  </span><span style="background: white; color: black">c</span><span style="background: white; color: gray">.</span><span style="background: white; color: magenta">object_id </span><span style="background: white; color: gray">= </span><span style="background: white; color: black">parent_object_id </span><span style="background: white; color: gray">and </span><span style="background: white; color: black">c</span><span style="background: white; color: gray">.</span><span style="background: white; color: black">column_id </span><span style="background: white; color: gray">= </span><span style="background: white; color: black">fc</span><span style="background: white; color: gray">.</span><span style="background: white; color: black">parent_column_id
</span><span style="background: white; color: blue">where        </span><span style="background: white; color: black">fc</span><span style="background: white; color: gray">.</span><span style="background: white; color: black">parent_object_id </span><span style="background: white; color: gray">= </span><span style="background: white; color: black">@tabelObjectId </span><span style="background: white; color: gray">and </span><span style="background: white; color: black">c</span><span style="background: white; color: gray">.</span><span style="background: white; color: black">name </span><span style="background: white; color: gray">= </span><span style="background: white; color: black">@ColumnName

</span><span style="background: white; color: blue">declare </span><span style="background: white; color: black">@ForeignKeyName </span><span style="background: white; color: blue">int
set </span><span style="background: white; color: black">@ForeignKeyName </span><span style="background: white; color: gray">= (</span><span style="background: white; color: blue">select </span><span style="background: white; color: black">name </span><span style="background: white; color: blue">from </span><span style="background: white; color: green">sys</span><span style="background: white; color: gray">.</span><span style="background: white; color: green">objects </span><span style="background: white; color: blue">where </span><span style="background: white; color: magenta">object_id </span><span style="background: white; color: gray">= </span><span style="background: white; color: black">@ForeignKeyObjectId</span><span style="background: white; color: gray">)

</span><span style="background: white; color: blue">if </span><span style="background: white; color: magenta">object_id</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">@ForeignKeyObjectId</span><span style="background: white; color: gray">) is not null
</span><span style="background: white; color: blue">begin
    exec</span><span style="background: white; color: gray">(</span><span style="background: white; color: red">'alter table ' + @TableName + ' drop constraint ' </span><span style="background: white; color: gray">+ </span><span style="background: white; color: black">@ForeignKeyName</span><span style="background: white; color: gray">)
</span><span style="background: white; color: blue">end</span></pre>
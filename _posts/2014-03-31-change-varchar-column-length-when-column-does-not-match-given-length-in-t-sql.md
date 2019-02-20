---
ID: 3712
post_title: >
  Change varchar column length, when
  column does not match given length in
  T-SQL.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/03/31/change-varchar-column-length-when-column-does-not-match-given-length-in-t-sql/
published: true
post_date: 2014-03-31 08:58:06
---
<p>The following code will update a column to varchar(max) only, when it does not already have the varchar(max) length.</p>   <pre class="code"><span style="background: white; color: green">-- Update column 'Name' length, it should be varchar(max).
-- Note: varchar(max) has length '-1'.
</span><span style="background: white; color: blue">if </span><span style="background: white; color: gray">(    
        (
            </span><span style="background: white; color: blue">select </span><span style="background: white; color: black">character_maximum_length
            </span><span style="background: white; color: blue">from </span><span style="background: white; color: green">information_schema</span><span style="background: white; color: gray">.</span><span style="background: white; color: green">columns
            </span><span style="background: white; color: blue">where </span><span style="background: white; color: black">table_name</span><span style="background: white; color: gray">=</span><span style="background: white; color: magenta">object_name</span><span style="background: white; color: gray">(</span><span style="background: white; color: magenta">object_id</span><span style="background: white; color: gray">(</span><span style="background: white; color: red">'dbo.Table1'</span><span style="background: white; color: gray">))
            and </span><span style="background: white; color: black">COLUMN_NAME </span><span style="background: white; color: gray">= </span><span style="background: white; color: red">'Name'
        </span><span style="background: white; color: gray">) &lt;&gt; -</span><span style="background: white; color: black">1
    </span><span style="background: white; color: gray">)
</span><span style="background: white; color: blue">begin
    alter table </span><span style="background: white; color: black">dbo</span><span style="background: white; color: gray">.</span><span style="background: white; color: black">Table1 </span><span style="background: white; color: blue">alter column </span><span style="background: white; color: black">Name </span><span style="background: white; color: blue">varchar</span><span style="background: white; color: gray">(</span><span style="background: white; color: magenta">max</span><span style="background: white; color: gray">) not null
</span><span style="background: white; color: blue">end</span></pre>
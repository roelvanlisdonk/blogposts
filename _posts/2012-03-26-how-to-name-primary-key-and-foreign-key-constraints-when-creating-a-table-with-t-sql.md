---
ID: 2640
post_title: >
  How to name primary key and foreign key
  constraints, when creating a table with
  T-SQL.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/03/26/how-to-name-primary-key-and-foreign-key-constraints-when-creating-a-table-with-t-sql/
published: true
post_date: 2012-03-26 16:53:45
---
<p>When trouble shouting error’s thrown by T-SQL, naming your primary and foreign keys, proves to be handy.</p>  <p align="left">When creating tables with T-SQL, I use the naming format PK_MyTable_MyColumn1_MyColumn2 and FK_MyTable_MyColumn3_MyColumn4:</p>   <pre class="code"><span style="color: blue">if </span><span style="color: magenta">object_id</span><span style="color: gray">(</span><span style="color: red">'[dbo].[Address]'</span><span style="color: gray">) is null
</span><span style="color: blue">begin
    create table </span><span style="color: teal">[dbo]</span><span style="color: gray">.</span><span style="color: teal">[Address]
    </span><span style="color: gray">(
        </span><span style="color: teal">Id        </span><span style="color: blue">int </span><span style="color: gray">not null  </span><span style="color: blue">identity</span><span style="color: gray">(</span>1<span style="color: gray">,</span>1<span style="color: gray">) </span><span style="color: blue">constraint </span><span style="color: teal">PK_Address_Id </span><span style="color: blue">primary key
    </span><span style="color: gray">)
</span><span style="color: blue">end


if </span><span style="color: magenta">object_id</span><span style="color: gray">(</span><span style="color: red">'[dbo].[Person]'</span><span style="color: gray">) is null
</span><span style="color: blue">begin
  create table </span><span style="color: teal">[dbo]</span><span style="color: gray">.</span><span style="color: teal">[Person]
  </span><span style="color: gray">(
      </span><span style="color: teal">Id           </span><span style="color: blue">int </span><span style="color: gray">not null  </span><span style="color: blue">identity</span><span style="color: gray">(</span>1<span style="color: gray">,</span>1<span style="color: gray">) </span><span style="color: blue">constraint </span><span style="color: teal">PK_Person_Id </span><span style="color: blue">primary key</span><span style="color: gray">,
      </span><span style="color: teal">AddressId    </span><span style="color: blue">int </span><span style="color: gray">not null </span><span style="color: blue">constraint </span><span style="color: teal">FK_Person_AddressId </span><span style="color: blue">foreign key references </span><span style="color: teal">[dbo]</span><span style="color: gray">.</span><span style="color: teal">[Address]</span><span style="color: gray">(</span><span style="color: teal">Id</span><span style="color: gray">)
  )
</span><span style="color: blue">end
</span></pre>
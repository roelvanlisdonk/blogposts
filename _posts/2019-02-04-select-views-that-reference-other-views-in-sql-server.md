---
ID: 5337
post_title: >
  Select views that reference other views
  in SQL Server
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2019/02/04/select-views-that-reference-other-views-in-sql-server/
published: true
post_date: 2019-02-04 12:22:53
---
<p>
 </p><p style="background: white"><span style="color:green; font-family:Consolas; font-size:10pt">-- Select views that reference other views.<span style="color:black">
			</span></span></p><p style="background: white"><span style="color:blue; font-family:Consolas; font-size:10pt">select distinct<span style="color:black">
			</span></span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">            s.[name]
</span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">,           v.[name]
</span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">,           r.referenced_schema_name
</span></p><p style="background: white"><span style="color:black; font-family:Consolas; font-size:10pt">,           r.referenced_entity_name 
</span></p><p style="background: white"><span style="color:blue; font-family:Consolas; font-size:10pt">from<span style="color:black">        sys.views v
</span></span></p><p style="background: white"><span style="color:blue; font-family:Consolas; font-size:10pt">join<span style="color:black">        sys.schemas s <span style="color:blue">on<span style="color:black"> v.schema_id = s.schema_id
</span></span></span></span></p><p style="background: white"><span style="color:blue; font-family:Consolas; font-size:10pt">cross<span style="color:black">
				<span style="color:blue">apply<span style="color:black"> sys.dm_sql_referenced_entities (s.[name] +  <span style="color:#a31515">'.'<span style="color:black"> + v.[name], <span style="color:#a31515">'OBJECT'<span style="color:black">) r
</span></span></span></span></span></span></span></span></p><p style="background: white"><span style="color:blue; font-family:Consolas; font-size:10pt">join<span style="color:black">        sys.objects o <span style="color:blue">on<span style="color:black"> r.referenced_id = o.object_id
</span></span></span></span></p><p style="background: white"><span style="color:blue; font-family:Consolas; font-size:10pt">where<span style="color:black">       o.[type] = <span style="color:#a31515">'V'<span style="color:black">
					</span></span></span></span></p><p style="background: white"><span style="color:blue; font-family:Consolas; font-size:10pt">order by<span style="color:black">    s.[name], v.[name]
</span></span></p>
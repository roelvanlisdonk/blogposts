---
ID: 3349
post_title: >
  How to get the full stored procedure
  name (incl. schema name) within the
  current executing stored procedure.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/08/29/how-to-get-the-full-stored-procedure-name-incl-schema-name-within-the-current-executing-stored-procedure/
published: true
post_date: 2013-08-29 13:27:11
---
<p>&#160;</p>  <p>Here is a function you can use to get the full stored procedure name (incl. schema name) within the current executing stored procedure:</p>   <p>&#160;</p>  <pre class="code"><span style="background: white; color: blue">if  </span><span style="background: white; color: magenta">object_id</span><span style="background: white; color: gray">(</span><span style="background: white; color: red">'dbo.GetFullSprocName'</span><span style="background: white; color: gray">) is not null
</span><span style="background: white; color: blue">begin
    drop function </span><span style="background: white; color: black">dbo</span><span style="background: white; color: gray">.</span><span style="background: white; color: black">GetFullSprocName
</span><span style="background: white; color: blue">end
go

create function </span><span style="background: white; color: black">dbo</span><span style="background: white; color: gray">.</span><span style="background: white; color: black">GetFullSprocName </span><span style="background: white; color: gray">(</span><span style="background: white; color: black">@sprocId </span><span style="background: white; color: blue">int</span><span style="background: white; color: gray">)
</span><span style="background: white; color: blue">returns varchar</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">255</span><span style="background: white; color: gray">)
</span><span style="background: white; color: blue">as
begin
    declare </span><span style="background: white; color: black">@FullSprocName </span><span style="background: white; color: blue">as varchar</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">255</span><span style="background: white; color: gray">)
    
    </span><span style="background: white; color: blue">set </span><span style="background: white; color: black">@FullSprocName </span><span style="background: white; color: gray">= (
        </span><span style="background: white; color: blue">select        top </span><span style="background: white; color: black">1 s</span><span style="background: white; color: gray">.</span><span style="background: white; color: black">name </span><span style="background: white; color: gray">+ </span><span style="background: white; color: red">'.' </span><span style="background: white; color: gray">+ </span><span style="background: white; color: black">o</span><span style="background: white; color: gray">.</span><span style="background: white; color: black">name
        </span><span style="background: white; color: blue">from        </span><span style="background: white; color: green">sys</span><span style="background: white; color: gray">.</span><span style="background: white; color: green">objects </span><span style="background: white; color: black">o </span><span style="background: white; color: blue">with</span><span style="background: white; color: gray">(</span><span style="background: white; color: blue">nolock</span><span style="background: white; color: gray">)
        inner join    </span><span style="background: white; color: green">sys</span><span style="background: white; color: gray">.</span><span style="background: white; color: green">schemas </span><span style="background: white; color: black">s </span><span style="background: white; color: blue">with </span><span style="background: white; color: gray">(</span><span style="background: white; color: blue">nolock</span><span style="background: white; color: gray">) </span><span style="background: white; color: blue">on </span><span style="background: white; color: black">o</span><span style="background: white; color: gray">.</span><span style="background: white; color: magenta">schema_id </span><span style="background: white; color: gray">= </span><span style="background: white; color: black">s</span><span style="background: white; color: gray">.</span><span style="background: white; color: magenta">schema_id
        </span><span style="background: white; color: blue">where        </span><span style="background: white; color: black">o</span><span style="background: white; color: gray">.</span><span style="background: white; color: magenta">object_id </span><span style="background: white; color: gray">= </span><span style="background: white; color: black">@sprocId
    </span><span style="background: white; color: gray">)

    </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">@FullSprocName
</span><span style="background: white; color: blue">end
go

</span></pre>

<p>To call this function use:</p>

<p>&#160;</p>

<pre class="code"><span style="background: white; color: blue">declare </span><span style="background: white; color: black">@sprocName </span><span style="background: white; color: blue">varchar</span><span style="background: white; color: gray">(</span><span style="background: white; color: black">128</span><span style="background: white; color: gray">) = </span><span style="background: white; color: black">dbo</span><span style="background: white; color: gray">.</span><span style="background: white; color: black">GetFullSprocName</span><span style="background: white; color: gray">(</span><span style="background: white; color: magenta">@@PROCID</span><span style="background: white; color: gray">)</span></pre>
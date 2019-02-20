---
ID: 3182
post_title: >
  Drop all stored procedures not belonging
  to the dbo schema from a SQL Server
  database
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/04/05/drop-all-stored-procedures-not-belonging-to-the-dbo-schema-from-a-sql-server-database/
published: true
post_date: 2013-04-05 10:37:29
---
<p>if you want to drop all stored procedures not belonging to the dbo schema from a SQL Server database, you van use the following select statement to generate a list that can be executed to drop the sprocs.</p>  <p>PS: It’s your foot.</p>  <p>&#160;</p>  <pre class="code"><span style="background: white; color: blue">    select        </span><span style="background: white; color: red">'drop procedure ' </span><span style="background: white; color: gray">+ </span><span style="background: white; color: black">s</span><span style="background: white; color: gray">.</span><span style="background: white; color: black">name </span><span style="background: white; color: gray">+ </span><span style="background: white; color: red">'.' </span><span style="background: white; color: gray">+ </span><span style="background: white; color: black">o</span><span style="background: white; color: gray">.</span><span style="background: white; color: black">name
    </span><span style="background: white; color: blue">from          </span><span style="background: white; color: green">sys</span><span style="background: white; color: gray">.</span><span style="background: white; color: green">objects </span><span style="background: white; color: black">o </span><span style="background: white; color: blue">with </span><span style="background: white; color: gray">(</span><span style="background: white; color: blue">nolock</span><span style="background: white; color: gray">)
    inner join    </span><span style="background: white; color: green">sys</span><span style="background: white; color: gray">.</span><span style="background: white; color: green">schemas </span><span style="background: white; color: black">s </span><span style="background: white; color: blue">with </span><span style="background: white; color: gray">(</span><span style="background: white; color: blue">nolock</span><span style="background: white; color: gray">) </span><span style="background: white; color: blue">on </span><span style="background: white; color: black">o</span><span style="background: white; color: gray">.</span><span style="background: white; color: magenta">schema_id </span><span style="background: white; color: gray">= </span><span style="background: white; color: black">s</span><span style="background: white; color: gray">.</span><span style="background: white; color: magenta">schema_id
    </span><span style="background: white; color: blue">where         </span><span style="background: white; color: black">o</span><span style="background: white; color: gray">.</span><span style="background: white; color: blue">type </span><span style="background: white; color: gray">= </span><span style="background: white; color: red">'P'
    </span><span style="background: white; color: gray">and           </span><span style="background: white; color: black">s</span><span style="background: white; color: gray">.</span><span style="background: white; color: black">name </span><span style="background: white; color: gray">&lt;&gt; </span><span style="background: white; color: red">'dbo'</span></pre>
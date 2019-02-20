---
ID: 522
post_title: >
  How to grant exec rights to all stored
  procedures in Microsoft SQL Server 2005
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/06/09/how-to-grant-exec-rights-to-all-stored-procedures-in-microsoft-sql-server-2005/
published: true
post_date: 2009-06-09 15:58:12
---
<p>Users are in our case always a member of some role. The role is given exec stored procedure rights and db_datareader, db_datawriter rights.   <br />Users in the role “TestRole” can select, insert, update, delete data and execute storedprocedures and functions.    <br /></p>  <pre class="code"><span style="color: blue">if not exists </span>(<span style="color: blue">select </span>1 <span style="color: blue">from </span>dbo.sysusers su (<span style="color: blue">nolock</span>) <span style="color: blue">where </span>su.issqlrole = 1 <span style="color: blue">and </span>su.[name] = <span style="color: #a31515">'TestRole'</span>)
<span style="color: blue">begin
    create </span>role TestRole
    <span style="color: blue">grant execute to </span>TestRole
    <span style="color: blue">exec </span>sp_addrolemember db_datareader, PegasoServiceRole
    <span style="color: blue">exec </span>sp_addrolemember db_datawriter, PegasoServiceRole
<span style="color: blue">end</span></pre>
<a href="http://11011.net/software/vspaste"></a>
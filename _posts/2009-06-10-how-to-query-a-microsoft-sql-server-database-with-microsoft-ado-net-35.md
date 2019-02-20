---
ID: 532
post_title: >
  How to query a Microsoft SQL Server
  database with Microsoft ADO .NET 3.5
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/06/10/how-to-query-a-microsoft-sql-server-database-with-microsoft-ado-net-35/
published: true
post_date: 2009-06-10 15:23:50
---
<p>The following C# code will query a log table on a Microsoft SQL Server database by using Microsoft ADO .NET 3.5:   <br /><span style="color: blue">&#160;&#160;&#160;&#160;&#160;&#160;&#160; public bool </span>DoesLogTableContainMessage(<span style="color: blue">string</span>message)    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; {    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <span style="color: blue">bool </span>result = <span style="color: blue">false</span>;    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <span style="color: blue">using</span>(<span style="color: #2b91af">DataTable </span>dataTable = <span style="color: blue">new</span><span style="color: #2b91af">DataTable</span>())    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; {    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <span style="color: blue">using</span>(<span style="color: #2b91af">SqlConnection </span>connection = <span style="color: blue">new</span><span style="color: #2b91af">SqlConnection</span>(<span style="color: #2b91af">ConfigurationManager</span>.ConnectionStrings[<span style="color: #a31515">&quot;UnittestDb&quot;</span>].ConnectionString))    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; {    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; connection.Open();    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <span style="color: blue">using</span>(<span style="color: #2b91af">SqlDataAdapter </span>adapter = <span style="color: blue">new</span><span style="color: #2b91af">SqlDataAdapter</span>(<span style="color: #a31515">&quot;select * from adalog where [message] like 'test%'&quot;</span>, connection))    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; {    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <span style="color: blue">int </span>rowsAffected = adapter.Fill(dataTable);    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; }    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; }    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <span style="color: blue">if</span>(dataTable.Rows.Count &gt; 0)    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; result = <span style="color: blue">true</span>;    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; }    <br />    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <span style="color: blue">return</span>result;    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; }</p> <a href="http://11011.net/software/vspaste"></a>  <p>   <br />The following C# code will execute a truncate table on a log table on a Microsoft SQL Server database by using Microsoft ADO .NET 3.5:    <br /><span style="color: blue">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; using </span>(<span style="color: #2b91af">SqlConnection </span>connection = <span style="color: blue">new</span><span style="color: #2b91af">SqlConnection</span>(<span style="color: #2b91af">ConfigurationManager</span>.ConnectionStrings[<span style="color: #a31515">&quot;UnittestDb&quot;</span>].ConnectionString))    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; {    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; connection.Open();    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <span style="color: blue">using</span>(<span style="color: #2b91af">SqlCommand </span>command = <span style="color: blue">new</span><span style="color: #2b91af">SqlCommand</span>(<span style="color: #a31515">&quot;truncate table adalog&quot;</span>, connection))    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; {    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <span style="color: blue">int </span>rowsAffected = command.ExecuteNonQuery();    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; }    <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; }</p> <a href="http://11011.net/software/vspaste"></a>
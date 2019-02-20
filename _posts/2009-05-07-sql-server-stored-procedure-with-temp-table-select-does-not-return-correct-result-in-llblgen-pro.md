---
ID: 365
post_title: >
  SQL Server Stored Procedure with temp
  table select, does not return correct
  result in LLBLGen Pro
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/07/sql-server-stored-procedure-with-temp-table-select-does-not-return-correct-result-in-llblgen-pro/
published: true
post_date: 2009-05-07 07:55:13
---
<p>When you create a stored procedure like:</p><pre class="code"><span style="color:blue;">if </span><span style="color:gray;">exists (</span><span style="color:blue;">select </span>1 <span style="color:blue;">from </span><span style="color:green;">sysobjects </span><span style="color:blue;">where </span>name <span style="color:gray;">= </span><span style="color:red;">'GetDataFromTempTable' </span><span style="color:gray;">and </span>xtype <span style="color:gray;">= </span><span style="color:red;">'p'</span><span style="color:gray;">)
    </span><span style="color:blue;">drop procedure </span>[dbo]<span style="color:gray;">.</span>[GetDataFromTempTable]
<span style="color:blue;">go

create procedure </span>[dbo]<span style="color:gray;">.</span>[GetDataFromTempTable]
<span style="color:blue;">as
begin

</span><span style="color:green;">-- Create temp table
</span><span style="color:blue;">create table </span>#MyTempTable
<span style="color:gray;">(
    </span>[Id] <span style="color:blue;">int </span><span style="color:gray;">not null </span><span style="color:blue;">primary key</span><span style="color:gray;">,
    </span>[Nummer] <span style="color:blue;">varchar</span><span style="color:gray;">(</span>10<span style="color:gray;">) not null
)

</span><span style="color:blue;">insert </span>#MyTempTable <span style="color:gray;">(</span>[Id]<span style="color:gray;">, </span>[Nummer]<span style="color:gray;">) </span><span style="color:blue;">values </span><span style="color:gray;">(</span>1<span style="color:gray;">, </span><span style="color:red;">'Test1'</span><span style="color:gray;">)

</span><span style="color:green;">-- Return all rows from the temp table
</span><span style="color:blue;">select
    </span><span style="color:gray;">*
</span><span style="color:blue;">from
    </span>#MyTempTable

<span style="color:blue;">end
go</span></pre>
<p><a href="http://11011.net/software/vspaste"></a>&nbsp;</p>
<p>and generate code with LLBLGen Pro to call this stored procedure, <br />it will generate an Action Stored Procedure Call instead off a Retrieval Stored Procedure Call.<br />This is, because LLBLGen Pro by default automatically generates the return type. see<br /><a title="http://www.llblgen.com/documentation/2.6/using%20the%20designer/designer_creatingproject.htm" href="http://www.llblgen.com/documentation/2.6/using%20the%20designer/designer_creatingproject.htm">http://www.llblgen.com/documentation/2.6/using%20the%20designer/designer_creatingproject.htm</a><br /><br />By changing the user preference AutoDetermineSProcType to false, you can manually change the amount of result sets during the catalog refresh. </p>
<p><strong>Change AutoDetermineSProcType</strong><br />LLBLGen Pro &gt; File &gt; Preferences... &gt; AutoDetermineSProcType &gt; set to false<br /><br /><strong>Refresh catalog<br /></strong>LLBLGen Pro &gt; Project &gt; Refresh All Catalogs... &gt; Manually select the stored procedures to retrieve<br />&gt; New number of Resultsets for selected procedures &gt; set to 1</p>
<p><br />The stored procedure can now be added to Retrieval Stored Procedure Calls instead of Action Stored Procedure Calls.</p>
---
ID: 581
post_title: >
  Microsoft SQL Server Integration
  Services (SSIS) 2008 and logging with
  the SSIS log provider for SQL Server
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/07/30/microsoft-sql-server-integration-services-ssis-2008-and-logging-with-the-ssis-log-provider-for-sql-server/
published: true
post_date: 2009-07-30 14:59:15
---
<p>If you use the SSIS log provider for SQL Server in Microsoft SQL Server Integration Services (SSIS) 2008, the provider will create a table ‘sysssislog’ in the destination database. The table will be created with schema name. If the SSIS package is run under the “dbo” the table will be created as “<strong>dbo.sysssislog</strong>”, but if the package is run under a database user which is not “dbo” of the database the tabled will be created like: “<strong>Domain1\User2.sysssislog</strong>”. The system stored procedures that are used for logging, aspect de table schema name to be “dbo” en not “Domain1\User2”, so it will fail with error, see below.    <br />    <br />We use a sql server agent job to run a SSIS package. The job step is set to “Run as” a proxy account, which is authorized for the subsystem “SQL Server Integration Services Package”. The proxy is coupled to a credential, the credential is coupled to a windows account that has “Run as a Job” permissions and is member of the msdb database role “'SQLAgentUserRole”. The account that runs the SSIS package is not “dbo”, because the database is created by another account.</p>  <p>&#160;</p>  <p><strong>Workarround</strong>    <br />Because we want the database to be installed by user “Domain1\User1” and the “sql server agent job step that executes the SSIS package” to be run as user “Domain1\User2”, we can’t let the SSIS package create the table automatically. We create the table during database installation by the “Domain1\User1” account. The table is then created as “dbo.sysssislog”.    <br />    <br />    <br /><strong>Table create script     <br /></strong></p>  <pre class="code"><span style="color: blue">create table </span>[sysssislog](
      [id] [int] <span style="color: blue">identity</span>(1,1) <span style="color: blue">not null</span>,
      [event] [sysname] <span style="color: blue">not null</span>,
      [computer] [nvarchar](128) <span style="color: blue">not null</span>,
      [operator] [nvarchar](128) <span style="color: blue">not null</span>,
      [source] [nvarchar](1024) <span style="color: blue">not null</span>,
      [sourceid] [uniqueidentifier] <span style="color: blue">not null</span>,
      [executionid] [uniqueidentifier] <span style="color: blue">not null</span>,
      [starttime] [datetime] <span style="color: blue">not null</span>,
      [endtime] [datetime] <span style="color: blue">not null</span>,
      [datacode] [int] <span style="color: blue">not null</span>,
      [databytes] [image] <span style="color: blue">null</span>,
      [message] [nvarchar](2048) <span style="color: blue">not null</span>,
<span style="color: blue">primary key clustered
</span>(
      [id] <span style="color: blue">asc
</span>)<span style="color: blue">with </span>(PAD_INDEX  = <span style="color: blue">off</span>, STATISTICS_NORECOMPUTE  = <span style="color: blue">off</span>, IGNORE_DUP_KEY = <span style="color: blue">off</span>, ALLOW_ROW_LOCKS  = <span style="color: blue">on</span>, ALLOW_PAGE_LOCKS  = <span style="color: blue">on</span>) <span style="color: blue">on </span>[PRIMARY]
) <span style="color: blue">on </span>[PRIMARY] TEXTIMAGE_ON [PRIMARY]
go


<strong></strong></pre>

<p><strong>Error Message</strong>

  <br />Executed as user: <font color="#ff0000">Domain1\User2</font>. Microsoft (R) SQL Server Execute Package Utility&#160; Version 10.0.1600.22 for 64-bit&#160; Copyright (C) Microsoft Corp 1984-2005. All rights reserved.&#160;&#160;&#160; Started:&#160; 2:39:01 PM&#160; Error: 2009-07-30 14:39:03.59&#160;&#160;&#160;&#160; Code: 0xC0202009&#160;&#160;&#160;&#160; Source: Controleer nieuwe foutmeldingen Ophalen foutmeldingen [31]&#160;&#160;&#160;&#160; Description: SSIS Error Code DTS_E_OLEDBERROR.&#160; An OLE DB error has occurred. Error code: 0x80004005.&#160; An OLE DB record is available.&#160; Source: &quot;Microsoft SQL Server Native Client 10.0&quot;&#160; Hresult: 0x80004005&#160; Description: <font color="#ff0000">&quot;Invalid object name 'sysssislog'.&quot;.</font>&#160; End Error&#160; Error: 2009-07-30 14:39:03.59&#160;&#160;&#160;&#160; Code: 0xC020204A&#160;&#160;&#160;&#160; Source: Controleer nieuwe foutmeldingen Ophalen foutmeldingen [31]&#160;&#160;&#160;&#160; Description: <font color="#ff0000">Unable to retrieve column information from the data source. Make sure your target table in the database is available</font>.&#160; End Error&#160; Error: 2009-07-30 14:39:03.59&#160;&#160;&#160;&#160; Code: 0xC004706B&#160;&#160;&#160;&#160; Source: Controleer nieuwe foutmeldingen SSIS.Pipeline&#160;&#160;&#160;&#160; Description: &quot;component &quot;Ophalen foutmeldingen&quot; (31)&quot; failed validation and returned validation status &quot;VS_ISBROKEN&quot;.&#160; End Error&#160; Error: 2009-07-30 14:39:03.59&#160;&#160;&#160;&#160; Code: 0xC004700C&#160;&#160;&#160;&#160; Source: Controleer nieuwe foutmeldingen SSIS.Pipeline&#160;&#160;&#160;&#160; Description: One or more component failed validation.&#160; End Error&#160; Error: 2009-07-30 14:39:03.59&#160;&#160;&#160;&#160; Code: 0xC0024107&#160;&#160;&#160;&#160; Source: Controleer nieuwe foutmeldingen&#160;&#160;&#160;&#160;&#160; Description: There were errors during task validation.&#160; End Error&#160; DTExec: The package execution returned DTSER_FAILURE (1).&#160; Started:&#160; 2:39:01 PM&#160; Finished: 2:39:03 PM&#160; Elapsed:&#160; 2.109 seconds.&#160; The package execution failed.&#160; The step failed.</p>
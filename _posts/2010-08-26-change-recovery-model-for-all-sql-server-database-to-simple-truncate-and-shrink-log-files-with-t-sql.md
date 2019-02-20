---
ID: 1703
post_title: >
  Change recovery model for all SQL server
  database to Simple, truncate and shrink
  log files with T-SQL
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/08/26/change-recovery-model-for-all-sql-server-database-to-simple-truncate-and-shrink-log-files-with-t-sql/
published: true
post_date: 2010-08-26 08:56:31
---
<p>When you have many databases on a database development SQL server and these databases are re-creatable, you can save space by setting the recovery model for all databases to Simple, truncate and shrink the log files, with the following T-SQL script</p>  <pre class="code"><span style="color: green">/*
    Only use this script for SQL Server development servers!
    Script must be executed as sysadmin
     
    This script will execute the following actions on all databases
        - set recovery model to [Simple]
        - trucate log file
        - shrink log file
*/

</span><span style="color: blue">use </span>[master]
<span style="color: blue">go

</span><span style="color: green">-- Declare container variabels for each column we select in the cursor
</span><span style="color: blue">declare </span>@databaseName <span style="color: blue">nvarchar</span><span style="color: gray">(</span>128<span style="color: gray">)

</span><span style="color: green">-- Define the cursor name
</span><span style="color: blue">declare </span>databaseCursor <span style="color: blue">cursor
</span><span style="color: green">-- Define the dataset to loop
</span><span style="color: blue">for
select </span>[name] <span style="color: blue">from </span><span style="color: green">sys</span><span style="color: gray">.</span><span style="color: green">databases

-- Start loop
</span><span style="color: blue">open </span>databaseCursor

<span style="color: green">-- Get information from the first row
</span><span style="color: blue">fetch next from </span>databaseCursor <span style="color: blue">into </span>@databaseName

<span style="color: green">-- Loop until there are no more rows
</span><span style="color: blue">while </span><span style="color: magenta">@@fetch_status </span><span style="color: gray">= </span>0
<span style="color: blue">begin
    print </span><span style="color: red">'Setting recovery model to Simple for database [' </span><span style="color: gray">+ </span>@databaseName <span style="color: gray">+ </span><span style="color: red">']'
    </span><span style="color: blue">exec</span><span style="color: gray">(</span><span style="color: red">'alter database [' </span><span style="color: gray">+ </span>@databaseName <span style="color: gray">+ </span><span style="color: red">'] set recovery Simple'</span><span style="color: gray">)
    
    </span><span style="color: blue">print </span><span style="color: red">'Shrinking logfile for database [' </span><span style="color: gray">+ </span>@databaseName <span style="color: gray">+ </span><span style="color: red">']'
    </span><span style="color: blue">exec</span><span style="color: gray">(</span><span style="color: red">'
    use [' </span><span style="color: gray">+ </span>@databaseName <span style="color: gray">+ </span><span style="color: red">'];' </span><span style="color: gray">+</span><span style="color: red">'
    
    declare @logfileName nvarchar(128);
    set @logfileName = (
        select top 1 [name] from sys.database_files where [type] = 1
    );
    dbcc shrinkfile(@logfileName,1);
    '</span><span style="color: gray">)
    
    </span><span style="color: green">-- Get information from next row
    </span><span style="color: blue">fetch next from </span>databaseCursor <span style="color: blue">into </span>@databaseName
<span style="color: blue">end

</span><span style="color: green">-- End loop and clean up
</span><span style="color: blue">close </span>databaseCursor
<span style="color: blue">deallocate </span>databaseCursor
<span style="color: blue">go

</span></pre>
<a href="http://11011.net/software/vspaste"></a>
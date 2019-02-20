---
ID: 434
post_title: 'Microsoft SQL Server sp_add_jobserver error: de specified server does not exist'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/22/microsoft-sql-server-sp_add_jobserver-error-de-specified-server-does-not-exist/
published: true
post_date: 2009-05-22 12:30:47
---
<p>If you use the sp_add_jobserver don't use '.' as servername, use '(local)', else you will get the error: de specified server does not exist   <br />    <br />EXEC @ReturnCode = msdb.dbo.sp_add_jobserver @job_id = @jobId, @server_name = N'(local)'    <br />IF (@@ERROR &lt;&gt; 0 OR @ReturnCode &lt;&gt; 0) GOTO QuitWithRollback</p>
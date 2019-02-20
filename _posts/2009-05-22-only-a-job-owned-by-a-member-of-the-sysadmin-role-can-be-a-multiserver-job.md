---
ID: 435
post_title: >
  Only a job owned by a member of the
  sysadmin role can be a multiserver job.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/22/only-a-job-owned-by-a-member-of-the-sysadmin-role-can-be-a-multiserver-job/
published: true
post_date: 2009-05-22 12:32:24
---
<p>Msg 14544, Level 16, State 1, Procedure sp_add_jobserver, Line 68    <br />This job is owned by 'Domain1\User1'. Only a job owned by a member of the sysadmin role can be a multiserver job.     <br />    <br />This is a very odd exception. In mine case it was caused by the TSQL script:    <br /></p>  <pre class="code"><span style="color: blue">exec </span>@ReturnCode <span style="color: gray">= </span>msdb<span style="color: gray">.</span>dbo<span style="color: gray">.</span><span style="color: maroon">sp_add_jobserver </span>@job_id <span style="color: gray">= </span>@jobId<span style="color: gray">, </span>@server_name <span style="color: gray">= </span><span style="color: red">N'.\Instance1'</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>Changing the code to:
  <br />

  <br /><span style="color: blue">exec </span>@ReturnCode <span style="color: gray">= </span>msdb<span style="color: gray">.</span>dbo<span style="color: gray">.</span><span style="color: maroon">sp_add_jobserver </span>@job_id <span style="color: gray">= </span>@jobId<span style="color: gray">, </span>@server_name <span style="color: gray">= </span><span style="color: red">N'Server1\Instance1'</span>

  <br />

  <br />solved the problem. </p>

<p>The owner of this Microsoft SQL Server multiserver Agent Job is still <strong>not</strong> member of the server role ‘sysadmin’ and the SSIS package it calls is executed correctly. So it is possible to run a Microsoft SQL Server Integration Services packages with a Microsoft SQL Server Agent Job under a domain account which is not member of the server role ‘sysadmin’, just create the correct proxy, credential, login and user accounts and add them to the correct roles (SQLAgentUserRole), and grant the correct access for the proxy (SSIS).

  </p>
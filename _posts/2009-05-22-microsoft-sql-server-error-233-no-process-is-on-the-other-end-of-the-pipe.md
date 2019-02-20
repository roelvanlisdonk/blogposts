---
ID: 426
post_title: 'Microsoft SQL Server, Error: 233, No process is on the other end of the pipe'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/22/microsoft-sql-server-error-233-no-process-is-on-the-other-end-of-the-pipe/
published: true
post_date: 2009-05-22 08:58:39
---
<div class="padten">   <div class="ms-inputuserfield padfive seventyp">     <div>       <div class="ExternalClass9185D5057FFE4C4CAC412E997D0DA01F">         <p><strong>Problem</strong>            <br />When connecting with windows authentication, the following exception was thrown:            <br />            <br /><span style="color: #943634">A connection was successfully established with the server, but then an error occurred during the login process.              <br />(provider: Shared Memory Provider, error: 0 - No process is on the other end of the pipe.)               <br />(Microsoft SQL Server, Error: 233)</span>            <br />            <br /><strong>Solution</strong>            <br />Turns out the user had a default database that no longer existed.             <br />Changing the default database to Master solved the problem</p>       </div>     </div>   </div> </div>
---
ID: 422
post_title: 'Named Pipes before TCP/IP causes &quot;SQL Server does not exist or access denied&quot; error message'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/22/named-pipes-before-tcpip-causes-sql-server-does-not-exist-or-access-denied-error-message/
published: true
post_date: 2009-05-22 08:41:09
---
<div class="padten">   <div class="ms-inputuserfield padfive seventyp">     <div>       <div class="ExternalClass64545EA1F50A4B8780867D9478670EFA">         <p><strong>Applies to Microsoft SQL Server 2000             <br /></strong>If Named Pipes come before TCP/IP in the SQl Server Client Network Utility, you can get the error message &quot;SQL Server does not exist or access denied&quot;, when you try to connect remotely to your Microsoft SQL Server 2000 instance. When you connect localy on the server everything seems to work fine.            <br /><strong>             <br />Solution              <br /></strong>Disable all network protocols except TCP/IP in the SQl Server Client Network Utility            <br />Restart the service of your Micorosft SQL Server 2000 instance.</p>       </div>     </div>   </div> </div>
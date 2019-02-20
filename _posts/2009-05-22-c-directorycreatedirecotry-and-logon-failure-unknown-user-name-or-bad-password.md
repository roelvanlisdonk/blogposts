---
ID: 414
post_title: 'C# &#8211; Directory.CreateDirecotry and Logon failure: unknown user name or bad password.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/22/c-directorycreatedirecotry-and-logon-failure-unknown-user-name-or-bad-password/
published: true
post_date: 2009-05-22 07:48:19
---
<p>   <br />When you want to create a folder on a network share on an other domain with the code Directory.CreateDirectory(@&quot;<a>\\nas\test</a>&quot;)     <br />, you can get a exception [Logon failure: unknown user name or bad password.]     <br />Giving Full Control Permissions to the Everyone account does not solve the problem, because the application pool account is using a domain account [A] and the share     <br />needs domain account [B] permissions</p>  <p>   <br /><strong>Solution</strong>     <br />Create domain account [A] (eg. DOMAIN_A\User1 with password 12345A)     <br />Create domain account [B] (eg. DOMAIN_B\User1 with password 12345A)     <br />Make sure the application pool identity = DOMAIN_A\User1     <br />Make sure the domain account DOMAIN_B\User1 has full control permissions on NetwerkShare &quot;<a>\\nas</a>&quot;     <br />or use impersonation in C# code (domain account DOMAIN_B\User1 with password 12345A)</p>
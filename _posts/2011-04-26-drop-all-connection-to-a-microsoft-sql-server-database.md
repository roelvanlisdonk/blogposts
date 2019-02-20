---
ID: 1995
post_title: >
  Drop all connection to a Microsoft SQL
  Server database
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/04/26/drop-all-connection-to-a-microsoft-sql-server-database/
published: true
post_date: 2011-04-26 13:56:04
---
<p>To drop all connections to a Microsoft SQL Server database use:</p>  <p style="padding-bottom: 0px; line-height: normal; margin: 0cm 0cm 0pt; text-autospace: ; mso-layout-grid-align: none" class="MsoNormal" align="left"><font face="Courier New"><span style="font-family: ; color: ; mso-ansi-language: en-us; mso-no-proof: yes" lang="EN-US"><font color="#0000ff"><font style="font-size: 10pt">alter</font></font></span><span style="font-family: ; mso-ansi-language: en-us; mso-no-proof: yes" lang="EN-US"><font style="font-size: 10pt"><font color="#000000"> </font><span style="color: "><font color="#0000ff">database</font></span><font color="#000000"> [DATABASE_NAME]</font></font></span></font></p>  <p style="padding-bottom: 0px; line-height: normal; margin: 0cm 0cm 0pt; text-autospace: ; mso-layout-grid-align: none" class="MsoNormal" align="left"><font face="Courier New"><span style="font-family: ; color: ; mso-ansi-language: en-us; mso-no-proof: yes" lang="EN-US"><font color="#0000ff"><font style="font-size: 10pt">set</font></font></span><span style="font-family: ; mso-ansi-language: en-us; mso-no-proof: yes" lang="EN-US"><font style="font-size: 10pt"><font color="#000000"> </font></font><span style="color: "><font style="font-size: 10pt" color="#0000ff">single_user</font></span></span></font></p>  <p style="padding-bottom: 0px; line-height: 13pt; margin: 0cm 0cm 10pt" class="MsoNormal" align="left"><font face="Courier New"><span style="line-height: 12pt; font-family: ; color: ; mso-no-proof: yes"><font color="#0000ff"><font style="font-size: 10pt">with</font></font></span><span style="line-height: 12pt; font-family: ; mso-no-proof: yes"><font style="font-size: 10pt"><font color="#000000"> </font><span style="color: "><font color="#0000ff">rollback</font></span><font color="#000000"> immediate</font></font></span></font></p>
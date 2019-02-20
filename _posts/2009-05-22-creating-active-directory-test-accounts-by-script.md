---
ID: 431
post_title: >
  Creating active directory test accounts
  by script
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/22/creating-active-directory-test-accounts-by-script/
published: true
post_date: 2009-05-22 11:14:34
---
<p>For creating active directory test accounts you can make use of the dsadd tool.   <br /><b>Dsadd</b> is a command-line tool that is built into Windows Server 2008. It is available if you have the Active Directory Domain Services (AD DS) server role installed. To use <b>dsadd</b>, you must run the <b>dsadd</b> command from an elevated command prompt. To open an elevated command prompt, click <b>Start</b>, right-click <b>Command Prompt</b>, and then click <b>Run as administrator</b>.</p>  <p><strong>Create an user with UserName 111111 and Password TestPassword40</strong></p>  <p>dsadd user CN=111111,OU=TestUsers,DC=TEST,DC=local -pwd TestPassword40</p>  <p>See</p>  <p><a href="http://technet2.microsoft.com/windowsserver/en/library/8d37ecb0-ac28-4e05-aa05-da82dc36b54b1033.mspx?mfr=true">http://technet2.microsoft.com/windowsserver/en/library/8d37ecb0-ac28-4e05-aa05-da82dc36b54b1033.mspx?mfr=true</a></p>  <p><strong>Dsrm</strong></p>  <p>Deleting users can be done by using the dsrm tool.   <br />Deletes an object of a specific type or any general object from the directory.</p>  <p><b>Dsrm</b> is a command-line tool that is built into Windows Server 2008. It is available if you have the Active Directory Domain Services (AD DS) or Active Directory Lightweight Directory Services (AD LDS) server role installed. To use <b>dsrm</b>, you must run the <b>dsrm</b> command from an elevated command prompt. To open an elevated command prompt, click <b>Start</b>, right-click <b>Command Prompt</b>, and then click <b>Run as administrator</b>. </p>  <p><strong>Delete an user with UserName 111111</strong></p>  <p>dsrm -noprompt CN=111111,OU=TestUsers,DC=TEST,DC=local</p>
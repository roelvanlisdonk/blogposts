---
ID: 1150
post_title: >
  Show password in plaintext, by using
  Get-Credential in PowerShell
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/23/show-password-in-plaintext-by-using-get-credential-in-powershell/
published: true
post_date: 2010-03-23 15:15:19
---
<p>&#160;</p>  <p>To show the password from the Get-Credentials cmdlet in plaintext,&#160; use the following PowerShell script:</p>  <p>&#160;</p>  <p>$credential = Get-Credential</p>  <p>[Runtime.InteropServices.Marshal]::PtrToStringAuto([Runtime.InteropServices.Marshal]::SecureStringToBSTR($credential .Password))</p>
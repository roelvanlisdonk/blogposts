---
ID: 1742
post_title: 'Solving the error: MyApplication.exe has encountered a problem and needs to close.  We are sorry for the inconvenience in a C# application'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/09/29/solving-the-error-myapplication-exe-has-encountered-a-problem-and-needs-to-close-we-are-sorry-for-the-inconvenience-in-a-c-application/
published: true
post_date: 2010-09-29 11:00:19
---
<p align="left">I was getting the error: <strong>MyApplication.exe has encountered a problem and needs to close.&#160; We are sorry for the inconvenience</strong>, but I was not getting any unhandled exceptions in my “HandleGlobalExceptions” event:</p>  <p align="left">&#160;</p>  <p align="left">AppDomain.CurrentDomain.UnhandledException += HandleGlobalExceptions; </p>  <p align="left">&#160;</p>  <p align="left">After setting some MessageBox.Show(&quot;Step 1&quot;) statements, I could see that the application was entering an endless loop. The code was accessing a property get in the property get it self.</p>  <p align="left">This was the cause of the error message. So no exception will be thrown, but the .net framework simply shows you the message:</p>  <p align="left">MyApplication.exe has encountered a problem and needs to close.&#160; We are sorry for the inconvenience</p>
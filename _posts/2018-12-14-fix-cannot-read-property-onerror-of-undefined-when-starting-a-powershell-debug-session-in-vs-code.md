---
ID: 5293
post_title: 'Fix: Cannot read property ‘onError’ of undefined, when starting a PowerShell debug session in VS Code'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2018/12/14/fix-cannot-read-property-onerror-of-undefined-when-starting-a-powershell-debug-session-in-vs-code/
published: true
post_date: 2018-12-14 10:47:22
---
I got the error: Cannot read property 'onError' of undefined, when starting a PowerShell debug session in VS Code.

Removing the VS Live Share plugin fixed the problem, see also:

<a href="https://github.com/Microsoft/vscode/issues/61649">https://github.com/Microsoft/vscode/issues/61649</a>

<img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2018/12/121418_0947_FixCannotre1.png" alt="" />
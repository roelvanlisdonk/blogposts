---
ID: 363
post_title: >
  Microsoft Visual Studio bat and cmd file
  encoding problems
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/04/22/microsoft-visual-studio-bat-and-cmd-file-encoding-problems/
published: true
post_date: 2009-04-22 07:14:50
---
<p>When you create a bat or cmd file in Microsoft Visual Studio 2008 it will be saved as UTF-8 encoding, but bat files should have ASCII enconding.<br />Running a bat file starting with @echo off, creates an error:<br /><br />'∩╗┐@echo' is not recognized as an internal or external command, operable program or batch file.<br /><br />Saving the file as ASCII in Microsoft Visual Studio 2008 solved the problem<br /><br /><a title="http://code-journey.com/2008/12/22/visual-studio-2008-text-file-encoding-problems/" href="http://code-journey.com/2008/12/22/visual-studio-2008-text-file-encoding-problems/">http://code-journey.com/2008/12/22/visual-studio-2008-text-file-encoding-problems/</a></p>
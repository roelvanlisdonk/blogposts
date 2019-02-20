---
ID: 871
post_title: 'How to solve: IE 8 new tab hang on Connecting… on Windows 7 x64'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/12/23/how-to-solve-ie-8-new-tab-hang-on-connecting-on-windows-7-x64/
published: true
post_date: 2009-12-23 10:29:18
---
The solution posted on: <a title="http://social.answers.microsoft.com/Forums/en-US/InternetExplorer/thread/e312e580-1cbc-496b-8c6b-b69b8535a7bb" href="http://social.answers.microsoft.com/Forums/en-US/InternetExplorer/thread/e312e580-1cbc-496b-8c6b-b69b8535a7bb">http://social.answers.microsoft.com/Forums/en-US/InternetExplorer/thread/e312e580-1cbc-496b-8c6b-b69b8535a7bb</a> solved my problem

For Win 7 64 bits :
1 - Create a new notepad document and paste this text :
<em>@echo off
echo.
echo IEREREG Version 1.07 for IE8 27.03.2009
echo by Kai Schaetzl </em><a href="http://iefaq.info"><em>http://iefaq.info</em></a>
<em>echo installs and registers (if suitable) all DLLs known to be used by IE8.
echo should only take a few seconds, but please be patient
echo.
REM ******************************
echo registering IE files
REM IE files (= part of setup)
regsvr32 /s /i browseui.dll
REM regsvr32 /s /i browseui.dll,NI (unnecessary)
regsvr32 /s corpol.dll
regsvr32 /s dxtmsft.dll
regsvr32 /s dxtrans.dll
REM simple HTML Mail API
regsvr32 /s "%ProgramFiles(x86)%\internet explorer\hmmapi.dll"
REM group policy snap-in
regsvr32 /s ieaksie.dll
REM smart screen
regsvr32 /s ieapfltr.dll
REM ieak branding
regsvr32 /s iedkcs32.dll
REM dev tools
regsvr32 /s "%ProgramFiles(x86)%\internet explorer\iedvtool.dll"
regsvr32 /s iepeers.dll
REM Symptom: IE8 closes immediately on launch, missing from IE7
regsvr32 /s "%ProgramFiles(x86)%\internet explorer\ieproxy.dll"
REM no install point anymore
REM regsvr32 /s /i iesetup.dll
REM no reg point anymore
REM regsvr32 /s imgutil.dll
regsvr32 /s /i /n inetcpl.cpl
REM no install point anymore
REM regsvr32 /s /i inseng.dll
regsvr32 /s jscript.dll
REM license manager
regsvr32 /s licmgr10.dll
REM regsvr32 /s msapsspc.dll
REM regsvr32 /s mshta.exe
REM VS debugger
regsvr32 /s msdbg2.dll
REM no install point anymore
REM regsvr32 /s /i mshtml.dll
regsvr32 /s mshtmled.dll
regsvr32 /s msident.dll
REM no reg point anymore
REM regsvr32 /s msrating.dll
REM multimedia timer
regsvr32 /s mstime.dll
REM no install point anymore
REM regsvr32 /s /i occache.dll
REM process debug manager
regsvr32 /s "%ProgramFiles(x86)%\internet explorer\pdm.dll"
REM no reg point anymore
REM regsvr32 /s pngfilt.dll
REM regsvr32 /s /i setupwbv.dll (not there anymore!)
regsvr32 /s tdc.ocx
regsvr32 /s /i urlmon.dll
REM regsvr32 /s /i urlmon.dll,NI,HKLM
regsvr32 /s vbscript.dll
REM VML renderer
regsvr32 /s "%CommonProgramFiles%\microsoft shared\vgx\vgx.dll"
REM no install point anymore
REM regsvr32 /s /i webcheck.dll
regsvr32 /s /i /n wininet.dll
REM ******************************
echo registering system files
REM additional system dlls known to be used by IE
REM added 11.05.2006 Symptom: Add-Ons-Manager menu entry is present but nothing happens
regsvr32 /s extmgr.dll
REM added 12.05.2006 Symptom: Javascript links don't work (Robin Walker) .NET hub file
regsvr32 /s mscoree.dll
REM added 23.03.2009 Symptom: Find on this page is blank
regsvr32 /s oleacc.dll
REM added 24.03.2009 Symptom: Printing problems, open in new window
regsvr32 /s ole32.dll
REM mscorier.dll
REM mscories.dll
REM Symptom: open in new tab/window not working
regsvr32 /s actxprxy.dll
regsvr32 /s asctrls.ocx
regsvr32 /s cdfview.dll
regsvr32 /s comcat.dll
regsvr32 /s /i /n comctl32.dll
regsvr32 /s cryptdlg.dll
regsvr32 /s /i /n digest.dll
regsvr32 /s dispex.dll
regsvr32 /s hlink.dll
regsvr32 /s mlang.dll
regsvr32 /s mobsync.dll
regsvr32 /s /i msieftp.dll
REM regsvr32 /s msnsspc.dll #no entry point
regsvr32 /s msr2c.dll
regsvr32 /s msxml.dll
regsvr32 /s oleaut32.dll
REM regsvr32 /s plugin.ocx #no entry point
regsvr32 /s proctexe.ocx
REM plus DllRegisterServerEx ExA ExW ... ?
regsvr32 /s /i scrobj.dll
REM shdocvw.dll hasn't been updated for IE7 and IE8, it still registers itself for the Windows Internet Controls
regsvr32 /s /i shdocvw.dll
regsvr32 /s sendmail.dll
REM ******************************
REM PKI/crypto functionality
REM initpki can take very long to run and is rarely a problem
REM if there are problems with crypto, SSL, certificates
REM remove the three following REMs from the lines
REM echo We are almost done except one crypto file
REM echo but this will take very long, be patient!
REM regsvr32 /s /i:A initpki.dll
REM ******************************
REM tabbed browser, do at the end, why originally with /n ?
regsvr32 /s /i ieframe.dll
REM ******************************
echo correcting bugs in the registry
REM do some corrective work
REM Symptom: new tabs page cannot display content because it cannot access the controls (added 27. 3.2009)
REM This is a result of a bug in shdocvw.dll (see above), probably only on Windows XP
reg add "HKCR\TypeLib\{EAB22AC0-30C1-11CF-A7EB-0000C05BAE0B}\1.1\0\win32" /ve /t REG_SZ /d %systemroot%\system32\ieframe.dll /f
REM ******************************
echo all tasks have been finished
echo.
pause
</em>2 - Close all your IE windows and processes.
3 - Save your document on your Desktop by example, with the .bat extension. Right-click on it, and select "Run as administrator".
4 - Test if this tip resolved your issue by openning IE. If you use a Windows 32 bits version, please replace <em>%ProgramFiles(x86)%</em> by <em>%ProgramFiles%</em> in your .bat file.
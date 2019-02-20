---
ID: 4326
post_title: 'Use formatting&ndash;f, when writing to the output console with PowerShell'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/05/05/use-formattingf-when-writing-to-the-output-console-with-powershell/
published: true
post_date: 2015-05-05 12:18:21
---
<p>If you want to format a string when echoing to the screen, use parentheses.</p>  <p>Echo(&quot;This is {0} &quot; -f &quot;a test.&quot;)</p>  <p>&#160;</p>  <p>Will output:</p>  <p>This is a test. </p>  <p>&#160;</p>  <p>Note</p>  <p><a title="http://stackoverflow.com/questions/17623644/what-is-the-difference-between-echo-and-write-host-in-powershell" href="http://stackoverflow.com/questions/17623644/what-is-the-difference-between-echo-and-write-host-in-powershell">http://stackoverflow.com/questions/17623644/what-is-the-difference-between-echo-and-write-host-in-powershell</a></p>  <p><code>echo</code> is an alias for <code>Write-Output</code>, which writes to the Success output stream. This allows output to be processed through pipelines or redirected into files. <code>Write-Host</code> writes directly to the console, so the output can't be redirected/processed any further.</p>
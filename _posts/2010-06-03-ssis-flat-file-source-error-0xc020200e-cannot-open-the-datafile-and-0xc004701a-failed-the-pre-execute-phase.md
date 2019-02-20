---
ID: 1441
post_title: 'SSIS Flat File Source Error: 0xC020200E Cannot open the datafile and 0xC004701A failed the pre-execute phase'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/06/03/ssis-flat-file-source-error-0xc020200e-cannot-open-the-datafile-and-0xc004701a-failed-the-pre-execute-phase/
published: true
post_date: 2010-06-03 10:00:19
---
<p>I was getting an error when importing a csv file, by using the SSIS Flat File Source.</p>  <p>&#160;</p>  <p><strong>Error</strong></p>  <p>Error: 0xC020200E at Read Flat File [18]: Cannot open the datafile &quot;&quot;.   <br />Error: 0xC004701A at Import File, SSIS.Pipeline: component &quot;Read Flat File&quot; (18) failed the pre-execute phase and returned error code 0xC020200E.</p>  <p>&#160;</p>  <p><strong>Cause</strong></p>  <p>This was because the flat file source connection string was created by an expression. The expression used a parameter and this parameter was empty.</p>  <p>&#160;</p>  <p><strong>Solution</strong></p>  <p>When the parameter was filled with the correct value, eg “C:\Data\Test.csv”, the error was solved.</p>
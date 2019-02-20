---
ID: 2109
post_title: 'Solving the SSIS error: The PrimeOutput method on component &quot;&hellip;&quot; (107) returned error code 0x80131502.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/06/28/solving-the-ssis-error-the-primeoutput-method-on-component-107-returned-error-code-0x80131502/
published: true
post_date: 2011-06-28 13:30:50
---
<p>I was getting the errors:</p>  <p>&#160;</p>  <p><strong>Error 1</strong></p>  <p>SSIS Error Code DTS_E_THREADFAILED.</p>  <p>Thread &quot;SourceThread0&quot; has exited with error code 0xC0047038.</p>  <p>There may be error messages posted before this with more information on why the thread has exited.</p>  <p>&#160;</p>  <p><strong>Error 2</strong></p>  <p>SSIS Error Code DTS_E_PRIMEOUTPUTFAILED.</p>  <p>The PrimeOutput method on component &quot;SCR Read fout&quot; (107) returned error code 0x80131502.</p>  <p>The component returned a failure code when the pipeline engine called PrimeOutput(). </p>  <p>The meaning of the failure code is defined by the component, but the error is fatal and the pipeline stopped executing.</p>  <p>There may be error messages posted before this with more information about the failure.</p>  <p>&#160;</p>  <p><strong>Cause</strong></p>  <p>This was caused by a SSIS script component, that had a vb substring error in it.</p>  <p>&#160;</p>  <p><strong>Solution</strong></p>  <p>Fixing the substring exception fixed my problem.</p>
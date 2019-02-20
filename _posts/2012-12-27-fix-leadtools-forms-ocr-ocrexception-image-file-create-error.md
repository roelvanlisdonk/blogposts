---
ID: 3127
post_title: 'Fix: Leadtools.Forms.Ocr.OcrException. Image file create error.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/12/27/fix-leadtools-forms-ocr-ocrexception-image-file-create-error/
published: true
post_date: 2012-12-27 09:48:43
---
<p>If the Leadtools OCR engine is not started with the correct parameters, the exception &quot;Image file create error&quot; will be thrown. To fix this problem, make sure you start the OCR engine by executing the function Startup with parameter startupParameters set to the installation folder of Leadtools, like:</p>  <p>&#160;</p>  <pre class="code"><font color="#2b91af">IOcrEngine</font><span style="background: white; color: black"> ocrEngine = </span><span style="background: white; color: #2b91af">OcrEngineManager</span><span style="background: white; color: black">.CreateEngine(</span><span style="background: white; color: #2b91af">OcrEngineType</span><span style="background: white; color: black">.Plus, useThunkServer: </span><span style="background: white; color: blue">false</span><span style="background: white; color: black">);
ocrEngine.Startup(</span><span style="background: white; color: blue">null</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">, &quot;C:\Program Files (x86)\LeadTools\OCR Engine&quot;);</span></pre>
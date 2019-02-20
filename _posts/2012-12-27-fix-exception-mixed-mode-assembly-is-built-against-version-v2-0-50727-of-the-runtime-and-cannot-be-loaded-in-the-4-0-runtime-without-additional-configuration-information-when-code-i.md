---
ID: 3126
post_title: 'Fix: Exception &quot;Mixed mode assembly is built against version &#8216;v2.0.50727&#8217; of the runtime and cannot be loaded in the 4.0 runtime without additional configuration information.&quot;, when code is executed in a Microsoft Visual Studio 2012 test project.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/12/27/fix-exception-mixed-mode-assembly-is-built-against-version-v2-0-50727-of-the-runtime-and-cannot-be-loaded-in-the-4-0-runtime-without-additional-configuration-information-when-code-i/
published: true
post_date: 2012-12-27 09:21:52
---
<p align="left">When using an old version of LeadTools I encountered an exception during the execution of a Microsoft Visual Studio 2012 test. <strong>Mixed mode assembly is built against version 'v2.0.50727' of the runtime and cannot be loaded in the 4.0 runtime without additional configuration information.</strong> This error was fixed following the steps on <a title="http://blog.kristandyson.com/2012/05/encountering-systemiofileloadexception.html" href="http://blog.kristandyson.com/2012/05/encountering-systemiofileloadexception.html">http://blog.kristandyson.com/2012/05/encountering-systemiofileloadexception.html</a>.</p>  <p>&#160;</p>  <ol>   <li>Close Microsoft Visual Studio 2012 (and IIS express)</li>    <li>On Windows 8, start Notepad.exe as an administrator</li>    <li>     <div align="left">Open the file [C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\CommonExtensions\Microsoft\TestWindow\vstest.executionengine.x86.exe.config]</div>   </li>    <li>     <div align="left">Add and save:</div>   </li> </ol>  <p align="left">&#160;</p>  <p>&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot; ?&gt;   <br />&lt;configuration&gt;    <br />&#160; &lt;runtime&gt;    <br />&#160;&#160;&#160; &lt;legacyUnhandledExceptionPolicy enabled=&quot;1&quot;/&gt;    <br />&#160;&#160;&#160; &lt;assemblyBinding xmlns=&quot;urn:schemas-microsoft-com:asm.v1&quot;&gt;    <br />&#160;&#160;&#160;&#160;&#160; &lt;probing privatePath=&quot;Extensions&quot; /&gt;&#160;&#160;&#160;&#160;&#160; <br />&#160;&#160;&#160; &lt;/assemblyBinding&gt;    <br />&#160; &lt;/runtime&gt;    <br />&#160; &lt;system.diagnostics&gt;    <br />&#160;&#160;&#160; &lt;switches&gt;    <br />&#160;&#160;&#160;&#160;&#160; &lt;add name=&quot;TpTraceLevel&quot; value=&quot;0&quot; /&gt;    <br />&#160;&#160;&#160; &lt;/switches&gt;    <br />&#160; &lt;/system.diagnostics&gt;    <br />&#160; &lt;appSettings&gt;    <br />&#160;&#160;&#160; &lt;!--&lt;add key=&quot;ExecutionThreadApartmentState&quot; value =&quot;MTA&quot;/&gt;--&gt;    <br />&#160;&#160;&#160; &lt;!--&lt;add key=&quot;TraceLogMaxFileSizeInKb&quot; value =&quot;10240&quot;/&gt;--&gt;&#160; </p>  <p>&#160;&#160;&#160; &lt;!-- MsTest Adapter Specific AppSettings --&gt;   <br />&#160;&#160;&#160; &lt;add key=&quot;TestProjectRetargetTo35Allowed&quot; value=&quot;true&quot; /&gt;    <br />&#160;&#160; &lt;/appSettings&gt;    <br />&#160;&#160; <strong>&lt;startup useLegacyV2RuntimeActivationPolicy=&quot;true&quot;&gt;      <br />&#160;&#160;&#160;&#160;&#160; &lt;supportedRuntime version=&quot;v4.0&quot; sku=&quot;.NETFramework,Version=v4.0&quot;/&gt;       <br />&#160;&#160; &lt;/startup&gt;</strong>    <br />&lt;/configuration&gt;</p>
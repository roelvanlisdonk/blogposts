---
ID: 740
post_title: >
  Leadtools engine initialization error,
  or there is no appropriate license
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/10/06/leadtools-engine-initialization-error-or-there-is-no-appropriate-license/
published: true
post_date: 2009-10-06 14:30:46
---
<p>If you get the error:</p>  <p>Leadtools.Forms.Ocr.OcrException : Engine initialization error, or there is no appropriate license.   <br />at Leadtools.Forms.Ocr.Plus.OcrEngine.StartupEngine(String startupParameters)    <br />at Leadtools.Forms.Ocr.Plus.OcrEngine.Startup(RasterCodecs rasterCodecs, String workDirectory, String startupParameters)</p>  <p>make sure the ocr engine is started with the correct path to the installation of the Leadtools.</p>  <pre class="code"><span style="color: green"> // Start OCR-engine var </span>ocrEngine = <span style="color: #2b91af">OcrEngineManager</span>.CreateEngine(<span style="color: #2b91af">OcrEngineType</span>.Plus, <span style="color: blue">false</span>);
            <span style="color: blue">if </span>(!ocrEngine.IsStarted)
            {
                ocrEngine.Startup(<span style="color: blue">null</span>, <span style="color: blue">null</span>, @<span style="color: #2b91af">“C:\InstallationFolderLeadTools”</span>);
            }</pre>

<p>&#160;</p>

<p>The LeadTools OCR Engine should be installed in&#160; C:\InstallationFolderLeadTools.</p>

<p>&#160;</p>

<p><strong>Adding LeadTools installation folder to the PATH variable</strong></p>

<p>The error can some times be caused by the folder C:\InstallationFolderLeadTools not being in the PATH variable.</p>

<p>Add the [C:\InstallationFolderLeadTools] to the PATH variable.</p>

<p>Control Panel &gt; System &gt; Advanced System Settings</p>

<p>&#160;</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/01/image3.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/01/image_thumb3.png" width="481" height="607" /></a></p>

<p>&#160;</p>

<p>&#160;</p>

<p><strong>enable32BitAppOnWin64</strong></p>

<p>This error can also be caused by an IIS or IIS express application pool not running in 32-bit application mode.</p>

<p>&#160;</p>

<p><strong>IIS</strong></p>

<p>Change IIS Application Pool setting [Enable 32-bit Applications] to [<strong>True</strong>]</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/01/image2.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/01/image_thumb2.png" width="580" height="479" /></a></p>

<p>&#160;</p>

<p><strong>IIS Express</strong></p>

<p>Add <strong>enable32BitAppOnWin64=&quot;true&quot;</strong> in [<strong>C:\Users\User1\Documents\IISExpress\config\applicationhost.config</strong>].</p>

<p align="left"><font size="1">&lt;applicationPools&gt;</font></p>

<p align="left"><font size="1">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &lt;add name=&quot;Clr4IntegratedAppPool&quot; managedRuntimeVersion=&quot;v4.0&quot; managedPipelineMode=&quot;Integrated&quot; CLRConfigFile=&quot;%IIS_USER_HOME%\config\aspnet.config&quot; autoStart=&quot;true&quot; <b>enable32BitAppOnWin64=&quot;true&quot;</b>&gt;</font></p>

<p align="left"><font size="1">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &lt;processModel loadUserProfile=&quot;true&quot; /&gt;</font></p>

<p align="left"><font size="1">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &lt;/add&gt;</font></p>

<p align="left"><font size="1">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &lt;add name=&quot;Clr4ClassicAppPool&quot; managedRuntimeVersion=&quot;v4.0&quot; managedPipelineMode=&quot;Classic&quot; CLRConfigFile=&quot;%IIS_USER_HOME%\config\aspnet.config&quot; autoStart=&quot;true&quot; <strong>enable32BitAppOnWin64=&quot;true&quot;</strong>/&gt;</font></p>

<p align="left"><font size="1">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &lt;add name=&quot;Clr2IntegratedAppPool&quot; managedRuntimeVersion=&quot;v2.0&quot; managedPipelineMode=&quot;Integrated&quot; CLRConfigFile=&quot;%IIS_USER_HOME%\config\aspnet.config&quot; autoStart=&quot;true&quot; <strong>enable32BitAppOnWin64=&quot;true&quot;</strong>/&gt;</font></p>

<p align="left"><font size="1">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &lt;add name=&quot;Clr2ClassicAppPool&quot; managedRuntimeVersion=&quot;v2.0&quot; managedPipelineMode=&quot;Classic&quot; CLRConfigFile=&quot;%IIS_USER_HOME%\config\aspnet.config&quot; autoStart=&quot;true&quot; <strong>enable32BitAppOnWin64=&quot;true&quot;</strong>/&gt;</font></p>

<p align="left"><font size="1">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &lt;add name=&quot;UnmanagedClassicAppPool&quot; managedRuntimeVersion=&quot;&quot; managedPipelineMode=&quot;Classic&quot; autoStart=&quot;true&quot; <strong>enable32BitAppOnWin64=&quot;true&quot;</strong>/&gt;</font></p>

<p align="left"><font size="1">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &lt;applicationPoolDefaults managedRuntimeLoader=&quot;v4.0&quot;&gt;</font></p>

<p align="left"><font size="1">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &lt;processModel /&gt;</font></p>

<p align="left"><font size="1">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &lt;/applicationPoolDefaults&gt;</font></p>

<p align="left"><font size="1">&#160;&#160;&#160;&#160;&#160;&#160;&#160; &lt;/applicationPools&gt;</font></p>
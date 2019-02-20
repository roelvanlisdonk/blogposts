---
ID: 2713
post_title: >
  How to dynamically switch between IIS
  Express and full IIS in Microsoft Visual
  Studio 2010 by using a csproj.user file.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/05/24/how-to-dynamically-switch-between-iis-express-and-full-iis-in-microsoft-visual-studio-2010-by-using-a-csproj-user-file/
published: true
post_date: 2012-05-24 21:32:56
---
<p>If you want to give every developer the choice to use IIS Express or full IIS during development in Microsoft Visual Studio 2010 sp1, you can use a csproj.user file for you project. This file can be used to overwrite settings in the *.csproj file.</p>  <p>This file will by default not be added to TFS, so every developer can use it’s own configuration, without interfering with other developers.   <br />    <br />First uncheck &quot;Apply server settings to all users (store in project file)&quot;</p>  <p>Then check &quot;Use IIS Express&quot; on the Web tab from the Microsoft Visual Studio 2010 sp1 project.</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/05/image14.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/05/image_thumb14.png" width="580" height="494" /></a></p>  <p>&#160;</p>  <p>Change the generated *.csproj.user, like:</p>  <pre class="code"><span style="color: blue">&lt;?</span><span style="color: #a31515">xml </span><span style="color: red">version</span><span style="color: blue">=</span>&quot;<span style="color: blue">1.0</span>&quot; <span style="color: red">encoding</span><span style="color: blue">=</span>&quot;<span style="color: blue">utf-8</span>&quot;<span style="color: blue">?&gt;
&lt;</span><span style="color: #a31515">Project </span><span style="color: red">ToolsVersion</span><span style="color: blue">=</span>&quot;<span style="color: blue">4.0</span>&quot; <span style="color: red">xmlns</span><span style="color: blue">=</span>&quot;<span style="color: blue">http://schemas.microsoft.com/developer/msbuild/2003</span>&quot;<span style="color: blue">&gt;
  &lt;</span><span style="color: #a31515">PropertyGroup</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">ProjectView</span><span style="color: blue">&gt;</span>ShowAllFiles<span style="color: blue">&lt;/</span><span style="color: #a31515">ProjectView</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">UseIISExpress</span><span style="color: blue">&gt;</span>true<span style="color: blue">&lt;/</span><span style="color: #a31515">UseIISExpress</span><span style="color: blue">&gt;
  &lt;/</span><span style="color: #a31515">PropertyGroup</span><span style="color: blue">&gt;
  &lt;</span><span style="color: #a31515">ProjectExtensions</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">VisualStudio</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">FlavorProperties </span><span style="color: red">GUID</span><span style="color: blue">=</span>&quot;<span style="color: blue">{349c5851-65df-11da-9384-00065b846f21}</span>&quot;<span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">WebProjectProperties</span><span style="color: blue">&gt;
          &lt;</span><span style="color: #a31515">StartPageUrl</span><span style="color: blue">&gt;</span>Default.aspx<span style="color: blue">&lt;/</span><span style="color: #a31515">StartPageUrl</span><span style="color: blue">&gt;
          &lt;</span><span style="color: #a31515">StartAction</span><span style="color: blue">&gt;</span>SpecificPage<span style="color: blue">&lt;/</span><span style="color: #a31515">StartAction</span><span style="color: blue">&gt;
          &lt;</span><span style="color: #a31515">AspNetDebugging</span><span style="color: blue">&gt;</span>True<span style="color: blue">&lt;/</span><span style="color: #a31515">AspNetDebugging</span><span style="color: blue">&gt;
          &lt;</span><span style="color: #a31515">SilverlightDebugging</span><span style="color: blue">&gt;</span>False<span style="color: blue">&lt;/</span><span style="color: #a31515">SilverlightDebugging</span><span style="color: blue">&gt;
          &lt;</span><span style="color: #a31515">NativeDebugging</span><span style="color: blue">&gt;</span>False<span style="color: blue">&lt;/</span><span style="color: #a31515">NativeDebugging</span><span style="color: blue">&gt;
          &lt;</span><span style="color: #a31515">SQLDebugging</span><span style="color: blue">&gt;</span>False<span style="color: blue">&lt;/</span><span style="color: #a31515">SQLDebugging</span><span style="color: blue">&gt;
          &lt;</span><span style="color: #a31515">ExternalProgram</span><span style="color: blue">&gt;
          &lt;/</span><span style="color: #a31515">ExternalProgram</span><span style="color: blue">&gt;
          &lt;</span><span style="color: #a31515">StartExternalURL</span><span style="color: blue">&gt;
          &lt;/</span><span style="color: #a31515">StartExternalURL</span><span style="color: blue">&gt;
          &lt;</span><span style="color: #a31515">StartCmdLineArguments</span><span style="color: blue">&gt;
          &lt;/</span><span style="color: #a31515">StartCmdLineArguments</span><span style="color: blue">&gt;
          &lt;</span><span style="color: #a31515">StartWorkingDirectory</span><span style="color: blue">&gt;
          &lt;/</span><span style="color: #a31515">StartWorkingDirectory</span><span style="color: blue">&gt;
          &lt;</span><span style="color: #a31515">EnableENC</span><span style="color: blue">&gt;</span>False<span style="color: blue">&lt;/</span><span style="color: #a31515">EnableENC</span><span style="color: blue">&gt;
          &lt;</span><span style="color: #a31515">AlwaysStartWebServerOnDebug</span><span style="color: blue">&gt;</span>True<span style="color: blue">&lt;/</span><span style="color: #a31515">AlwaysStartWebServerOnDebug</span><span style="color: blue">&gt;
          <strong><font size="3">&lt;</font></strong></span><strong><font size="3"><span style="color: #a31515">UseIIS</span><span style="color: blue">&gt;</span>True<span style="color: blue">&lt;/</span><span style="color: #a31515">UseIIS</span></font></strong><span style="color: blue"><strong><font size="3">&gt;</font></strong>
          &lt;</span><span style="color: #a31515">AutoAssignPort</span><span style="color: blue">&gt;</span>False<span style="color: blue">&lt;/</span><span style="color: #a31515">AutoAssignPort</span><span style="color: blue">&gt;
          &lt;</span><span style="color: #a31515">DevelopmentServerPort</span><span style="color: blue">&gt;</span>1000<span style="color: blue">&lt;/</span><span style="color: #a31515">DevelopmentServerPort</span><span style="color: blue">&gt;
          &lt;</span><span style="color: #a31515">DevelopmentServerVPath</span><span style="color: blue">&gt;</span>/Test<span style="color: blue">&lt;/</span><span style="color: #a31515">DevelopmentServerVPath</span><span style="color: blue">&gt;
          <strong><font size="3">&lt;</font></strong></span><strong><font size="3"><span style="color: #a31515">IISUrl</span><span style="color: blue">&gt;</span>http://localhost:1000/Test<span style="color: blue">&lt;/</span><span style="color: #a31515">IISUrl</span></font></strong><span style="color: blue"><strong><font size="3">&gt;</font></strong>
          &lt;</span><span style="color: #a31515">NTLMAuthentication</span><span style="color: blue">&gt;</span>False<span style="color: blue">&lt;/</span><span style="color: #a31515">NTLMAuthentication</span><span style="color: blue">&gt;
          &lt;</span><span style="color: #a31515">UseCustomServer</span><span style="color: blue">&gt;</span>False<span style="color: blue">&lt;/</span><span style="color: #a31515">UseCustomServer</span><span style="color: blue">&gt;
          &lt;</span><span style="color: #a31515">CustomServerUrl</span><span style="color: blue">&gt;
          &lt;/</span><span style="color: #a31515">CustomServerUrl</span><span style="color: blue">&gt;
        &lt;/</span><span style="color: #a31515">WebProjectProperties</span><span style="color: blue">&gt;
      &lt;/</span><span style="color: #a31515">FlavorProperties</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">VisualStudio</span><span style="color: blue">&gt;
  &lt;/</span><span style="color: #a31515">ProjectExtensions</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">Project</span><span style="color: blue">&gt;
</span></pre>


<p>Now your build server can use the settings in the csproj file and you, as a developer, have the choice to use these settings or overwrite them with the *.csproj.user file.</p>
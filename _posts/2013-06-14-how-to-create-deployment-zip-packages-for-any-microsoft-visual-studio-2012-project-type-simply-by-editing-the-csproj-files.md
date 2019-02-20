---
ID: 3265
post_title: 'How to create deployment zip packages for any Microsoft Visual Studio 2012 project type, simply by editing the *.csproj files.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/06/14/how-to-create-deployment-zip-packages-for-any-microsoft-visual-studio-2012-project-type-simply-by-editing-the-csproj-files/
published: true
post_date: 2013-06-14 11:11:15
---
<p>If you want to create deployment zip packages for any Microsoft Visual Studio project type (like, Web Site, Web Service, Windows Service, Console Application etc. then just follow the steps below:</p>  <p>&#160;</p>  <p>In this example I will be zipping all content files and *.dll files found in the &quot;bin&quot; folder of an ASP .NET MVC 4 Web Application, but the same will work for other project types. This example will be using the MSBuild Community Zip Task and at this point will work for&#160; .NET projects &lt;= 4.5.</p>  <p>&#160;</p>  <h3>Create a new ASP .NET MVC 4 Web Application</h3>  <p>In Microsoft Visual Studio 2012, choose:</p>  <p>File &gt; New &gt; Project…</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image2.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image_thumb2.png" width="564" height="391" /></a></p>  <p>Choose Internet Application</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image3.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image_thumb3.png" width="502" height="528" /></a></p>  <p>&#160;</p>  <p>Add the nuget package&quot;MSBuild Community Tasks&quot;</p>  <p>Click click the solution in the Solution Explorer and choose &quot;Manage NuGet Packages for Solution…&quot;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image4.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image_thumb4.png" width="580" height="405" /></a></p>  <p>Choose MSBuildTasks</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image5.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image_thumb5.png" width="580" height="388" /></a></p>  <p>&#160;</p>  <p>&#160;</p>  <h3>Edit MSBuild.Community.Tasks.targets </h3>  <p>Edit the MSBuild.Community.Tasks.targets file, so it will use the MSBuild.Community.Tasks.dll found in the .build folder created by the NuGet package.</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image6.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image_thumb6.png" width="580" height="213" /></a></p>  <p>&#160;</p>  <p>Change:</p>  <pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: #a31515">MSBuildCommunityTasksLib</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">$(MSBuildCommunityTasksPath)\MSBuild.Community.Tasks.dll</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: #a31515">MSBuildCommunityTasksLib</span><span style="background: white; color: blue">&gt;</span></pre>

<p>To</p>

<pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: #a31515">MSBuildCommunityTasksLib</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">MSBuild.Community.Tasks.dll</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: #a31515">MSBuildCommunityTasksLib</span><span style="background: white; color: blue">&gt;</span></pre>

<p>Result</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image7.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image_thumb7.png" width="580" height="124" /></a></p>

<p>&#160;</p>

<p>&#160;</p>

<h3>Edit the *.csproj file</h3>

<p>Unload project (right click project &gt; Unload Project)</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image8.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image_thumb8.png" width="459" height="529" /></a></p>

<p>&#160;</p>

<p>Edit *.csproj file</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image9.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image_thumb9.png" width="502" height="330" /></a></p>

<p>Scroll to the bottom of the file and</p>

<p>change:</p>

<pre class="code"><span style="background: white; color: blue">&lt;!-- </span><span style="background: white; color: green">To modify your build process, add your task inside one of the targets below and uncomment it. 
       Other similar extension points exist, see Microsoft.Common.targets.
  &lt;Target Name=&quot;BeforeBuild&quot;&gt;
  &lt;/Target&gt;
  &lt;Target Name=&quot;AfterBuild&quot;&gt;
  &lt;/Target&gt; </span><span style="background: white; color: blue">--&gt;</span></pre>

<p>&#160;</p>

<p>To:</p>

<pre class="code"><p><span style="background: white; color: blue">  &lt;!-- </span><span style="background: white; color: green">Start Zip target </span><span style="background: white; color: blue">--&gt;
  &lt;</span><span style="background: white; color: #a31515">ItemGroup</span><span style="background: white; color: blue">&gt;
    &lt;!-- 
      </span><span style="background: white; color: green">Add all *.dll files found in the root of the &quot;bin&quot; folder as link files.
      - Use Files=&quot;@(Content);@(Link)&quot; in the zip target the include both content files as build output in the zip content. <br />      - Using the &quot;@(Content);@(Link)&quot; notation, will merge ItemGroup Content and ItemGroup Link into one property. </span><span style="background: white; color: green">
      - The &quot;.\&quot; before the &quot;bin&quot; folder name in the Include, results in a zip package containing the bin folder.
      - If you do not want to include the &quot;bin&quot; folder itself but only the files, use &quot;bin\*.dll&quot;.
      - If you want to include subfolders use &quot;.\bin\**\*.dll&quot;
    </span><span style="background: white; color: blue">--&gt;
    &lt;</span><span style="background: white; color: #a31515">Link </span><span style="background: white; color: red">Include</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">.\bin\*.dll</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: blue">/&gt;<br /><span style="background: white; color: blue">    &lt;</span><span style="background: white; color: #a31515">Link </span><span style="background: white; color: red">Include</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">.\bin\*.exe</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: blue">/&gt;<br /><span style="background: white; color: blue">    &lt;</span><span style="background: white; color: #a31515">Link </span><span style="background: white; color: red">Include</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">.\bin\*.exe.config</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: blue">/&gt;</span></span></span><span style="background: white; color: blue">
  &lt;/</span><span style="background: white; color: #a31515">ItemGroup</span><span style="background: white; color: blue">&gt;
  &lt;!-- 
    </span><span style="background: white; color: green">A relative path will start from the *.csproj file location, 
    so to get to the MSBuild.Community.Tasks.Targets file, we must add &quot;..\.build\&quot;.
  </span><span style="background: white; color: blue">--&gt;
  &lt;</span><span style="background: white; color: #a31515">Import </span><span style="background: white; color: red">Project</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">..\.build\MSBuild.Community.Tasks.Targets</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: blue">/&gt;
  &lt;!-- 
    </span><span style="background: white; color: green">The afterbuild target will only be executed, when the project is build in &quot;Release&quot; mode.
  </span><span style="background: white; color: blue">--&gt;
  &lt;</span><span style="background: white; color: #a31515">Target </span><span style="background: white; color: red">Name</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">AfterBuild</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">Condition</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">'$(Configuration)' == 'Release'</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: #a31515">PropertyGroup</span><span style="background: white; color: blue">&gt;
      &lt;</span><span style="background: white; color: #a31515">ReleasePath</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">bin</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: #a31515">ReleasePath</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: #a31515">PropertyGroup</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: #a31515">Zip </span><span style="background: white; color: red">Files</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">@(Content);@(Link)</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">WorkingDirectory</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">$(ReleasePath)</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">ZipFileName</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">output\$(AssemblyName).zip</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">ZipLevel</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">9</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: blue">/&gt;
  &lt;/</span><span style="background: white; color: #a31515">Target</span><span style="background: white; color: blue">&gt;
  &lt;!-- </span><span style="background: white; color: green">End Zip target </span><span style="background: white; color: blue">--&gt;</span></p></pre>

<p>&#160;</p>

<p>Reload project</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image10.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image_thumb10.png" width="493" height="414" /></a></p>

<p>&#160;</p>

<p><strong>Build project project in &quot;Release&quot; configuration</strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image11.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image_thumb11.png" width="580" height="76" /></a></p>

<p>&#160;</p>

<p>An output folder should be created containing the MVC1Application.zip.</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image12.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image_thumb12.png" width="364" height="406" /></a></p>

<p>&#160;</p>

<p>Zip file:</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image13.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image_thumb13.png" width="360" height="160" /></a></p>

<p>Extracted</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image14.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image_thumb14.png" width="386" height="244" /></a></p>
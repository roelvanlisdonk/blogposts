---
ID: 1644
post_title: 'Solving a fake &ldquo;This dependency cannot be added because it will create a circular dependency&rdquo; in Microsoft Visual Studio 2010'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/08/03/solving-a-fake-this-dependency-cannot-be-added-because-it-will-create-a-circular-dependency-in-microsoft-visual-studio-2010/
published: true
post_date: 2010-08-03 14:38:20
---
<p>When I wanted to add a project reference in Microsoft Visual Studio 2010, I was getting a “This dependency cannot be added because it will create a circular dependency” error message, but I was 100% sure this reference would not cause a circular dependency.</p>  <p>&#160;</p>  <p><img src="http://blogs.msdn.com/blogfiles/saraford/WindowsLiveWriter/DidyouknowHowtochangethebuildorderforyou_CB00/image_12.png" /></p>  <p>&#160;</p>  <p><strong>Solution</strong></p>  <p>I solved this problem by unloading the project in Microsoft Visual Studio, opened the *.csproj file in notepad.exe and added the project reference manually and reloaded the project.</p>  <p>&lt;ProjectReference Include=&quot;..\MyProject2\MyProject2.csproj&quot;&gt;   <br />&#160;&#160;&#160;&#160;&#160; &lt;Project&gt;{CD01F694-7705-4FE2-9610-D33C88862BE1}&lt;/Project&gt;    <br />&#160;&#160;&#160;&#160;&#160; &lt;Name&gt;MyProject2&lt;/Name&gt;    <br />&#160;&#160;&#160; &lt;/ProjectReference&gt;</p>  <p>The GUID can be found by opening the MyTest2.csproj and searching for the &lt;ProjectGuid&gt; tag.</p>
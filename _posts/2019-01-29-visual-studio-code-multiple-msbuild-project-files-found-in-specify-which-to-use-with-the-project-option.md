---
ID: 5326
post_title: 'Visual Studio Code &#8211; Multiple MSBuild project files found in &#8216;…&#8217;. Specify which to use with the &#8211;project option.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2019/01/29/visual-studio-code-multiple-msbuild-project-files-found-in-specify-which-to-use-with-the-project-option/
published: true
post_date: 2019-01-29 10:04:19
---
When developing, I like to have my tests in the same folder as the code and make the build process excluded test code for a production build (<span style="color: #92d050;">&lt;Compile Remove="**\*Test.cs" /&gt;</span>).
So I created a .NET Core command line application in Visual Studio Code (my.command.line.csproj) and placed a test project file inside the samen folder (my.command.line.test.csproj).

<strong>my.command.line.csproj
</strong>
<pre><code>

&lt;Project Sdk="Microsoft.NET.Sdk"&gt;

&lt;PropertyGroup&gt;

&lt;OutputType&gt;Exe&lt;/OutputType&gt;

&lt;TargetFramework&gt;netcoreapp2.2&lt;/TargetFramework&gt;

&lt;/PropertyGroup&gt;

&lt;ItemGroup&gt;

<span style="color: #92d050;"> &lt;Compile Remove="**\*Test.cs" /&gt;
</span>

&lt;/ItemGroup&gt;

&lt;/Project&gt;

<strong>my.command.line.test.csproj
</strong>

&lt;Project Sdk="Microsoft.NET.Sdk"&gt;

&lt;PropertyGroup&gt;

&lt;TargetFramework&gt;netcoreapp2.2&lt;/TargetFramework&gt;

&lt;IsPackable&gt;false&lt;/IsPackable&gt;

<span style="color: #00b050;">&lt;GenerateProgramFile&gt;false&lt;/GenerateProgramFile&gt;</span>

&lt;/PropertyGroup&gt;

&lt;ItemGroup&gt;

&lt;PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.9.0" /&gt;

&lt;PackageReference Include="MSTest.TestAdapter" Version="1.3.2" /&gt;

&lt;PackageReference Include="MSTest.TestFramework" Version="1.3.2" /&gt;

&lt;/ItemGroup&gt;

&lt;/Project&gt;
</code></pre>
Then I executed <strong>dotnet test</strong>

This will throw the following error:
<span style="color: red;">Program.cs(10,27): error CS0017: Program has more than one entry point defined. Compile with /main to specify the type that contains the entry point.</span>

This can be fixed by adding: <span style="color: #00b050;">&lt;GenerateProgramFile&gt;false&lt;/GenerateProgramFile&gt;</span> to a PropertyGroup inside the my.command.line.test.csproj.

Then when you execute <strong>dotnet test</strong> again, you will get the error:

<span style="color: red;">MSBUILD : error MSB1011: Specify which project or solution file to use because this folder contains more than one project or solution file.
</span>

To fix it, execute:
<strong>dotnet test "my.command.line.test.csproj"</strong>

When you execute <strong>dotnet watch test</strong>, you will first get the error

<span style="color: red;">Multiple MSBuild project files found in 'C:\Dev\'. Specify which to use with the --project option.
</span>

You might want to fix it like: <strong>dotnet watch --project "my.command.line.test.csproj" test</strong>, but then the watcher will start watching but you will get the error:<strong>
</strong>

<span style="color: red;">MSBUILD : error MSB1011: Specify which project or solution file to use because this folder contains more than one project or solution file.
</span>

<span style="color: red;">watch : Exited with error code 1
</span>

<span style="color: red;">watch : Waiting for a file to change before restarting dotnet...
</span>

To fix this, execute <strong>dotnet watch --project "my.command.line.test.csproj" test "my.command.line.test.csproj"</strong>

Now your tests will be executed and the tests will be re-executed, when any of the files change.
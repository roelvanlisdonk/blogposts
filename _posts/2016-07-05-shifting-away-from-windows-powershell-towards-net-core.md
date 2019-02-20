---
ID: 4956
post_title: >
  Shifting away from Windows PowerShell
  towards .NET Core
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2016/07/05/shifting-away-from-windows-powershell-towards-net-core/
published: true
post_date: 2016-07-05 13:23:16
---
<p>
 </p><p>Now that .NET Core 1.0 is released I find myself coding more and more in .NET Core instead of Windows PowerShell scripts for every day automation. When you are developing you spend a portion of your time setting up environments, renaming, copying, processing files and folders, for that I used to write Windows PowerShell scripts.
</p><p>
 </p><p>
 </p><p>With the release of .NET Core and its excellent command line and Visual Studio Code support, I'm writing plain old C#, but with dotnet run I can <strong>alter a C# file on the fly and run it immediately</strong>.
</p><p>Plus the C# code is <strong>portable between my Windows Desktop, Mac Book Pro laptop and Linux servers</strong>, very nice!
</p><p>
 </p><p>
 </p><p>
 </p><p>Some examples
</p><p>
 </p><p>
 </p><h3>Deleting *.css files (excluding the libraries folder)
</h3><p>When you are writing your code in CSS Next you want to keep the CSS Next files in source control, but you don't want to add the compiled css files in source control, to delete existing css files in a "App" folder, but not the css files in "App/Libraries" I wrote a little .NET Core code:
</p><p>
 </p><p><span style="color:blue; font-family:Consolas; font-size:9pt">public<span style="color:black">
				<span style="color:blue">void<span style="color:black"> DeleteCssFiles() {
</span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">string<span style="color:black"> projectFolder = <span style="color:maroon">@"C:\Projects\MyWebApp"<span style="color:black">;
</span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">string<span style="color:black"> appFolder = <span style="color:#2b91af">Path<span style="color:black">.Combine(projectFolder, <span style="color:#a31515">"App"<span style="color:black">);
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">string<span style="color:black"> librariesFolder = <span style="color:#2b91af">Path<span style="color:black">.Combine(appFolder, <span style="color:#a31515">"Libraries"<span style="color:black">);
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">string<span style="color:black"> csprojPath = <span style="color:#2b91af">Path<span style="color:black">.Combine(projectFolder, <span style="color:maroon">@" MyWebApp.csproj"<span style="color:black">);
</span></span></span></span></span></span></span></p><p>            
 </p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">int<span style="color:black"> fileCounter = 0;
</span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">var<span style="color:black"> files = FindFiles(<span style="color:blue">new<span style="color:black">
							<span style="color:#2b91af">DirectoryInfo<span style="color:black">(appFolder), <span style="color:#a31515">"*.css"<span style="color:black">); <span style="color:green">// This will get *.css and *.cssn files on Windows, don't know why.<span style="color:black">
												</span></span></span></span></span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">foreach<span style="color:black"> (<span style="color:#2b91af">FileInfo<span style="color:black"> file <span style="color:blue">in<span style="color:black"> files)
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">            {
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">if<span style="color:black">(
</span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">                    !file.FullName.StartsWith(librariesFolder) &amp;&amp;
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">                    !file.FullName.EndsWith(<span style="color:#a31515">".cssn"<span style="color:black">)
</span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">                ){
</span></p><p>                    
 </p><p><span style="color:black; font-family:Consolas; font-size:9pt">                    fileCounter++;
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:#2b91af">File<span style="color:black">.Delete(file.FullName);
</span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:#2b91af">Console<span style="color:black">.WriteLine(<span style="color:#a31515">$"Delete <span style="color:black">{file.FullName}<span style="color:#a31515">"<span style="color:black">);
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">                }
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">            }
</span></p><p>
 </p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:#2b91af">Console<span style="color:black">.WriteLine(<span style="color:#a31515">$"Total *.css files deleted = <span style="color:black">{fileCounter}<span style="color:#a31515">"<span style="color:black">);
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">        }
</span></p><p>
 </p><p>
 </p><h3>Rename all *.css files in the *.csproj file to *.cssn files (excluding the libraries folder) and make them build action "None"
</h3><p>
 </p><p><span style="color:blue; font-family:Consolas; font-size:9pt">Public async<span style="color:black">
				<span style="color:#2b91af">Task<span style="color:black"> RenameCssToCssnInCsProj() {
</span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">string<span style="color:black"> projectFolder = <span style="color:maroon">@"C:\Projects\MyWebApp "<span style="color:black">;
</span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">string<span style="color:black"> appFolder = <span style="color:#2b91af">Path<span style="color:black">.Combine(projectFolder, <span style="color:#a31515">"App"<span style="color:black">);
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">string<span style="color:black"> librariesFolder = <span style="color:#2b91af">Path<span style="color:black">.Combine(appFolder, <span style="color:#a31515">"Libraries"<span style="color:black">);
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">string<span style="color:black"> csprojPath = <span style="color:#2b91af">Path<span style="color:black">.Combine(projectFolder, <span style="color:maroon">@" MyWebApp.csproj"<span style="color:black">);
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">string<span style="color:black"> csprojContent = <span style="color:#2b91af">File<span style="color:black">.ReadAllText(csprojPath);
</span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">int<span style="color:black"> fileCounter = 0;
</span></span></span></p><p>
 </p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">var<span style="color:black"> files = FindFiles(<span style="color:blue">new<span style="color:black">
							<span style="color:#2b91af">DirectoryInfo<span style="color:black">(appFolder), <span style="color:#a31515">"*.css"<span style="color:black">); <span style="color:green">// This will get *.css and *.cssn files on Windows, don't know why.<span style="color:black">
												</span></span></span></span></span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">foreach<span style="color:black"> (<span style="color:#2b91af">FileInfo<span style="color:black"> file <span style="color:blue">in<span style="color:black"> files)
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">            {
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">var<span style="color:black"> cssnPath = <span style="color:#2b91af">Path<span style="color:black">.ChangeExtension(file.FullName, <span style="color:#a31515">".cssn"<span style="color:black">);
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">if<span style="color:black">(
</span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">                    !file.FullName.StartsWith(librariesFolder)                   
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">                ){
</span></p><p>                    
 </p><p><span style="color:black; font-family:Consolas; font-size:9pt">                    fileCounter++;
</span></p><p>
 </p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">string<span style="color:black"> relativePath = file.FullName.Replace(projectFolder + <span style="color:maroon">@"\"<span style="color:black">, <span style="color:blue">string<span style="color:black">.Empty);
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">string<span style="color:black"> relativePathCssn = <span style="color:#2b91af">Path<span style="color:black">.ChangeExtension(relativePath, <span style="color:#a31515">".cssn"<span style="color:black">);
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">string<span style="color:black"> find = <span style="color:#a31515">$"&lt;Content Include=\"<span style="color:black">{relativePath}<span style="color:#a31515">\" /&gt;"<span style="color:black">;
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">if<span style="color:black">(csprojContent.Contains(find))
</span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">                    {
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">string<span style="color:black"> replace = <span style="color:#a31515">$"&lt;None Include=\"<span style="color:black">{relativePathCssn}<span style="color:#a31515">\" /&gt;"<span style="color:black">;
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:#2b91af">Console<span style="color:black">.WriteLine(<span style="color:#a31515">$"find <span style="color:black">{find}<span style="color:#a31515">"<span style="color:black">);
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:#2b91af">Console<span style="color:black">.WriteLine(<span style="color:#a31515">$"replace <span style="color:black">{replace}<span style="color:#a31515">"<span style="color:black">);
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">                        csprojContent = csprojContent.Replace(find, replace);
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">                    }
</span></p><p>
 </p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">await<span style="color:black"> CreateOrUpdateFile(csprojPath, csprojContent);
</span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">                }
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">            }
</span></p><p>
 </p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:#2b91af">Console<span style="color:black">.WriteLine(<span style="color:#a31515">$"Total *.css files = <span style="color:black">{fileCounter}<span style="color:#a31515">"<span style="color:black">);
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">        }</span>
	</p><p>
 </p><p>
 </p><p>
 </p><h3>Converting all css files in a Web Application to CSS Next files (where each CSS Next file depends on a shared "variables.cssn" file.
</h3><p>
 </p><p>
 </p><p><span style="color:blue; font-family:Consolas; font-size:9pt">public<span style="color:black">
				<span style="color:blue">async<span style="color:black">
						<span style="color:#2b91af">Task<span style="color:black"> RenameCssToCssnOnDisk() {
</span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">string<span style="color:black"> projectFolder = <span style="color:maroon">@"C:\Projects\ZvdZ\zvdzonline\Source\ZvdZOnline\ZvdZOnline.Web"<span style="color:black">;
</span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">string<span style="color:black"> appFolder = <span style="color:#2b91af">Path<span style="color:black">.Combine(projectFolder, <span style="color:#a31515">"App"<span style="color:black">);
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">string<span style="color:black"> librariesFolder = <span style="color:#2b91af">Path<span style="color:black">.Combine(appFolder, <span style="color:#a31515">"Libraries"<span style="color:black">);
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">int<span style="color:black"> fileCounter = 0;
</span></span></span></p><p>            
 </p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">var<span style="color:black"> files = FindFiles(<span style="color:blue">new<span style="color:black">
							<span style="color:#2b91af">DirectoryInfo<span style="color:black">(projectFolder), <span style="color:#a31515">"*.css"<span style="color:black">); <span style="color:green">// This will get *.css and *.cssn files, don't know why.<span style="color:black">
												</span></span></span></span></span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">foreach<span style="color:black"> (<span style="color:#2b91af">FileInfo<span style="color:black"> file <span style="color:blue">in<span style="color:black"> files)
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">            {
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">var<span style="color:black"> cssnPath = <span style="color:#2b91af">Path<span style="color:black">.ChangeExtension(file.FullName, <span style="color:#a31515">".cssn"<span style="color:black">);
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">if<span style="color:black">(
</span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">                    !file.FullName.StartsWith(librariesFolder) &amp;&amp;
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">                    !<span style="color:#2b91af">File<span style="color:black">.Exists(cssnPath)
</span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">                ){
</span></p><p>                    
 </p><p><span style="color:black; font-family:Consolas; font-size:9pt">                    fileCounter++;
</span></p><p>
 </p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">string<span style="color:black"> relativePath = file.FullName.Replace(projectFolder, <span style="color:blue">string<span style="color:black">.Empty);
</span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:#2b91af">Console<span style="color:black">.WriteLine(<span style="color:#a31515">$"relativePath <span style="color:black">{relativePath}<span style="color:#a31515">"<span style="color:black">);
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">int<span style="color:black"> seperatorCounter = relativePath.Split(<span style="color:maroon">@"\"<span style="color:black">.ToCharArray()).Length - 1;
</span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:#2b91af">Console<span style="color:black">.WriteLine(<span style="color:#a31515">$"seperatorCounter <span style="color:black">{seperatorCounter}<span style="color:#a31515">"<span style="color:black">);
</span></span></span></span></span></span></span></p><p>                    
 </p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:green">// Determine the "import" variables line, that should be added to each CSS Next file.<span style="color:black">
				</span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">string<span style="color:black"> relativePrefix = <span style="color:blue">string<span style="color:black">.Empty;
</span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">for<span style="color:black">(<span style="color:blue">var<span style="color:black"> i = 0; i&lt; seperatorCounter; i++) {
</span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">                        relativePrefix += <span style="color:#a31515">"../"<span style="color:black">;
</span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">                    }
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">string<span style="color:black"> importText = <span style="color:#a31515">$"@import \"<span style="color:black">{relativePrefix}<span style="color:#a31515">App/Styles/variables.cssn\";"<span style="color:black">;
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:#2b91af">Console<span style="color:black">.WriteLine(<span style="color:#a31515">$"importText <span style="color:black">{importText}<span style="color:#a31515">"<span style="color:black">);
</span></span></span></span></span></span></span></p><p>                    
 </p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">string<span style="color:black"> content = <span style="color:#2b91af">File<span style="color:black">.ReadAllText(file.FullName);
</span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">await<span style="color:black"> CreateOrUpdateFile(cssnPath, importText + <span style="color:#2b91af">Environment<span style="color:black">.NewLine + <span style="color:#2b91af">Environment<span style="color:black">.NewLine + content );
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">                }
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">            }
</span></p><p>
 </p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:#2b91af">Console<span style="color:black">.WriteLine(<span style="color:#a31515">$"Total *.css files renamed = <span style="color:black">{fileCounter}<span style="color:#a31515">"<span style="color:black">);
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">        }</span>
	</p><p>
 </p><p>
 </p><p>
 </p><h3>Some Generic function used in the examples above
</h3><p>
 </p><p><span style="color:blue; font-family:Consolas; font-size:9pt">public<span style="color:black">
				<span style="color:blue">async<span style="color:black">
						<span style="color:#2b91af">Task<span style="color:black"> CreateOrUpdateFile(<span style="color:blue">string<span style="color:black"> path, <span style="color:blue">string<span style="color:black"> content)
</span></span></span></span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">        {
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">byte<span style="color:black">[] result = <span style="color:#2b91af">Encoding<span style="color:black">.UTF8.GetBytes(content);
</span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">using<span style="color:black"> (<span style="color:blue">var<span style="color:black"> stream = <span style="color:blue">new<span style="color:black">
									<span style="color:#2b91af">FileStream<span style="color:black">(path, <span style="color:#2b91af">FileMode<span style="color:black">.Create, <span style="color:#2b91af">FileAccess<span style="color:black">.Write, <span style="color:#2b91af">FileShare<span style="color:black">.Write, bufferSize: 4096, useAsync: <span style="color:blue">true<span style="color:black">))
</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">            {
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">await<span style="color:black"> stream.WriteAsync(result, 0, result.Length);
</span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">            }
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">        }
</span></p><p>
 </p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">public<span style="color:black">
					<span style="color:#2b91af">IEnumerable<span style="color:black">&lt;<span style="color:#2b91af">FileInfo<span style="color:black">&gt; FindFiles(<span style="color:#2b91af">DirectoryInfo<span style="color:black"> folder, <span style="color:blue">string<span style="color:black"> pattern)
</span></span></span></span></span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">        {
</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:green">// Note: using EnumerateFiles is faster then using "GetFiles".<span style="color:black">
				</span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">
			<span style="color:blue">return<span style="color:black"> folder.EnumerateFiles(pattern, <span style="color:#2b91af">SearchOption<span style="color:black">.AllDirectories);
</span></span></span></span></span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">        }</span>
	</p><p><span style="color:black; font-family:Consolas; font-size:9pt">
		</span> </p>
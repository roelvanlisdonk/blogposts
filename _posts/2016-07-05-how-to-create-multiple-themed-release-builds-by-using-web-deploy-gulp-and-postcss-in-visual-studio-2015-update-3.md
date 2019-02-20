---
ID: 4951
post_title: >
  How to create multiple themed release
  builds by using web deploy, gulp and
  PostCSS in Visual Studio 2015 update 3
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2016/07/05/how-to-create-multiple-themed-release-builds-by-using-web-deploy-gulp-and-postcss-in-visual-studio-2015-update-3/
published: true
post_date: 2016-07-05 11:33:20
---
<p> 
 </p><p><span style="color:#333333; font-family:Helvetica; font-size:10pt"><strong>Note </strong></span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p><span style="color:#333333; font-family:Helvetica; font-size:10pt">In this blogpost a "release build" is a folder containing all the files (html, css, JavaScript, images, dll's etc.) needed in production to run a specific themed web application. </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p> 
 </p><p> 
 </p><p> 
 </p><p><span style="color:#333333; font-family:Helvetica; font-size:10pt">The publish / deployment process in Visual Studio is intended to create one "release build", but I wanted this process to create 2 exactly the same "release builds", just with different themes (different images and css files). </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p> 
 </p><p><span style="color:#333333; font-family:Helvetica; font-size:10pt">To accomplish this, I altered / added / removed the following files: </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><ul style="margin-left: 44pt"><li><span style="color:#333333; font-family:Helvetica; font-size:10pt">Added deploy.pub.xml (the publish profile) </span>
		</li><li><div><span style="color:#333333; font-family:Helvetica; font-size:10pt">Altered the csproj file of the web project </span>
			</div><ul><li><div><span style="color:#333333; font-family:Helvetica; font-size:10pt">Added folder to the root "Themes" </span>
					</div><ul><li><div><span style="color:#333333; font-family:Helvetica; font-size:10pt">Theme1 </span>
							</div><ul><li><span style="color:#333333; font-family:Helvetica; font-size:10pt">Images (contains the images for this theme, build type = "None") </span>
								</li><li><span style="color:#333333; font-family:Helvetica; font-size:10pt">variables.cssn (contains all the css next variables for this theme, build type = "None") </span>
								</li></ul></li><li><div><span style="color:#333333; font-family:Helvetica; font-size:10pt">Theme2 </span>
							</div><ul><li><span style="color:#333333; font-family:Helvetica; font-size:10pt">Images (contains the images for this theme, build type = "None") </span>
								</li><li><span style="color:#333333; font-family:Helvetica; font-size:10pt">variables.cssn (contains all the css next variables for this theme, build type = "None") </span>
								</li></ul></li></ul></li></ul></li><li><span style="color:#333333; font-family:Helvetica; font-size:10pt">Added package.json (npm configuration file, build type = "None") </span>
		</li><li><span style="color:#333333; font-family:Helvetica; font-size:10pt">gulpfile.js (gulp configuration file, build type = "None") </span>
		</li><li><span style="color:#333333; font-family:Helvetica; font-size:10pt">gulpfile.helper.js (custom JavaScript code, build type = "None") </span>
		</li><li><span style="color:#333333; font-family:Helvetica; font-size:10pt">Renamed all *.css to *.cssn (css next) and set the build type = "None" (except the css files in the libraries folder) </span>
		</li><li><span style="color:#333333; font-family:Helvetica; font-size:10pt">Deleted all *.css files except the files in the libraries folder. </span>
		</li><li><span style="color:#333333; font-family:Helvetica; font-size:10pt">.gitignore </span>
		</li></ul><p> 
 </p><p> 
 </p><p> 
 </p><h3>Deploy.pubxml 
</h3><p> 
 </p><p><span style="color:#333333; font-family:Helvetica; font-size:10pt">Create a publishing file "deploy.pubxml" by right clicking on your web application project &gt; publish... &gt; Custom </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><ul style="margin-left: 62pt"><li><span style="color:#333333; font-family:Helvetica; font-size:10pt">Enter "deploy" for the name, his will create a deploy.pubxml. </span>
		</li><li><span style="color:#333333; font-family:Helvetica; font-size:10pt">Choose publish method "File System" </span>
		</li><li><span style="color:#333333; font-family:Helvetica; font-size:10pt">Enter a target location, for example C:\Release\MyWebApp </span>
		</li></ul><p> 
 </p><p> 
 </p><p> 
 </p><p><span style="color:blue; font-family:Consolas; font-size:9pt">&lt;?<span style="color:#a31515">xml<span style="color:blue">
					<span style="color:red">version<span style="color:blue">=<span style="color:black">"<span style="color:blue">1.0<span style="color:black">"<span style="color:blue">
											<span style="color:red">encoding<span style="color:blue">=<span style="color:black">"<span style="color:blue">utf-8<span style="color:black">"<span style="color:blue">?&gt;<span style="color:black">
																	</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Consolas; font-size:9pt">&lt;!--<span style="color:black">
			</span></span></p><p><span style="color:green; font-family:Consolas; font-size:9pt">This file is used by the publish/package process of your Web project. You can customize the behavior of this process<span style="color:black">
			</span></span></p><p><span style="color:green; font-family:Consolas; font-size:9pt">by editing this MSBuild file. In order to learn more about this please visit http://go.microsoft.com/fwlink/?LinkID=208121. <span style="color:black">
			</span></span></p><p><span style="color:blue; font-family:Consolas; font-size:9pt">--&gt;<span style="color:black">
			</span></span></p><p><span style="color:blue; font-family:Consolas; font-size:9pt">&lt;<span style="color:#a31515">Project<span style="color:blue">
					<span style="color:red">ToolsVersion<span style="color:blue">=<span style="color:black">"<span style="color:blue">4.0<span style="color:black">"<span style="color:blue">
											<span style="color:red">xmlns<span style="color:blue">=<span style="color:black">"<span style="color:blue">http://schemas.microsoft.com/developer/msbuild/2003<span style="color:black">"<span style="color:blue">&gt;<span style="color:black">
																	</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Consolas; font-size:9pt">  &lt;<span style="color:#a31515">PropertyGroup<span style="color:blue">&gt;<span style="color:black">
					</span></span></span></span></p><p><span style="color:blue; font-family:Consolas; font-size:9pt">    &lt;<span style="color:#a31515">WebPublishMethod<span style="color:blue">&gt;<span style="color:black">FileSystem<span style="color:blue">&lt;/<span style="color:#a31515">WebPublishMethod<span style="color:blue">&gt;<span style="color:black">
									</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Consolas; font-size:9pt">    &lt;<span style="color:#a31515">SiteUrlToLaunchAfterPublish<span style="color:blue"> /&gt;<span style="color:black">
					</span></span></span></span></p><p><span style="color:blue; font-family:Consolas; font-size:9pt">    &lt;<span style="color:#a31515">publishUrl<span style="color:blue">&gt;<span style="color:black">C:\Release\Theme1<span style="color:blue">&lt;/<span style="color:#a31515">publishUrl<span style="color:blue">&gt;<span style="color:black">
									</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Consolas; font-size:9pt">    &lt;<span style="color:#a31515">DeleteExistingFiles<span style="color:blue">&gt;<span style="color:black">False<span style="color:blue">&lt;/<span style="color:#a31515">DeleteExistingFiles<span style="color:blue">&gt;<span style="color:black">
									</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Consolas; font-size:9pt">    &lt;<span style="color:#a31515">LastUsedBuildConfiguration<span style="color:blue"> /&gt;<span style="color:black">
					</span></span></span></span></p><p><span style="color:blue; font-family:Consolas; font-size:9pt">    &lt;<span style="color:#a31515">LastUsedPlatform<span style="color:blue"> /&gt;<span style="color:black">
					</span></span></span></span></p><p><span style="color:blue; font-family:Consolas; font-size:9pt">    &lt;<span style="color:#a31515">LaunchSiteAfterPublish<span style="color:blue">&gt;<span style="color:black">False<span style="color:blue">&lt;/<span style="color:#a31515">LaunchSiteAfterPublish<span style="color:blue">&gt;<span style="color:black">
									</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Consolas; font-size:9pt">    &lt;<span style="color:#a31515">ExcludeApp_Data<span style="color:blue">&gt;<span style="color:black">False<span style="color:blue">&lt;/<span style="color:#a31515">ExcludeApp_Data<span style="color:blue">&gt;<span style="color:black">
									</span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Consolas; font-size:9pt">  &lt;/<span style="color:#a31515">PropertyGroup<span style="color:blue">&gt;<span style="color:black">
					</span></span></span></span></p><p><span style="color:blue; font-family:Consolas; font-size:9pt">  &lt;!--<span style="color:green">
				<span style="color:black">
				</span></span></span></p><p><span style="color:green; font-family:Consolas; font-size:9pt">    The target "GatherAllFilesToPublish" is the last target run by msbuild, before msdeploy starts copying files to the destination folder. <span style="color:black">
			</span></span></p><p><span style="color:green; font-family:Consolas; font-size:9pt">    This is the last time we can alter the output, because there is no "after publish" target.<span style="color:black">
			</span></span></p><p><span style="color:green; font-family:Consolas; font-size:9pt">    We have to use the property "AfterTargets", because "DependsOnTargets" doesn't work.<span style="color:black">
			</span></span></p><p>    
 </p><p><span style="color:green; font-family:Consolas; font-size:9pt">    The target runs a gulp task which creates a release output folder per theme (by using PostCSS and copying images to correct location).<span style="color:black">
			</span></span></p><p><span style="color:green; font-family:Consolas; font-size:9pt">      - themes:         Is a "comma" seperated list of themed releases that should be created<span style="color:black">
			</span></span></p><p><span style="color:green; font-family:Consolas; font-size:9pt">                        - The first item should be the "default" theme<span style="color:black">
			</span></span></p><p><span style="color:green; font-family:Consolas; font-size:9pt">      - projectFolder:  The folder containing the *.csproj file.<span style="color:black">
			</span></span></p><p><span style="color:green; font-family:Consolas; font-size:9pt">                        This folder is needed, because among other things it contains:<span style="color:black">
			</span></span></p><p><span style="color:green; font-family:Consolas; font-size:9pt">                        - the *.cssn (css next) files that should be compiled to *.css<span style="color:black">
			</span></span></p><p><span style="color:green; font-family:Consolas; font-size:9pt">                        - the theme images that should be copied<span style="color:black">
			</span></span></p><p><span style="color:green; font-family:Consolas; font-size:9pt">      - packageTempDir: The temp folder used by Visual Studio to create a release. This folder will be used as base for the other themed releases.<span style="color:black">
			</span></span></p><p><span style="color:green; font-family:Consolas; font-size:9pt">      - publishFolder:  Is set to the "publishUrl",<span style="color:black">
			</span></span></p><p><span style="color:green; font-family:Consolas; font-size:9pt">                        - The publishing process of Visual Studio is intended to work for one "release build".<span style="color:black">
			</span></span></p><p><span style="color:green; font-family:Consolas; font-size:9pt">                        - We are creating multiple "release builds", one for each theme.<span style="color:black">
			</span></span></p><p><span style="color:green; font-family:Consolas; font-size:9pt">                        - Each "release build" will be placed inside the parent folder of the "publishFolder"<span style="color:black">
			</span></span></p><p><span style="color:green; font-family:Consolas; font-size:9pt">                        - Only the first theme (default theme) will be placed directly into the "publishFolder"<span style="color:black">
			</span></span></p><p>    
 </p><p><span style="color:green; font-family:Consolas; font-size:9pt">    NOTE<span style="color:black">
			</span></span></p><p><span style="color:green; font-family:Consolas; font-size:9pt">      - npm run "gulp", will only work when the package.json contains scripts { "gulp": "gulp" }.<span style="color:black">
			</span></span></p><p><span style="color:green; font-family:Consolas; font-size:9pt">
			<span style="color:blue">--&gt;<span style="color:black">
				</span></span></span></p><p><span style="color:blue; font-family:Consolas; font-size:9pt">  &lt;<span style="color:#a31515">Target<span style="color:blue">
					<span style="color:red">Name<span style="color:blue">=<span style="color:black">"<span style="color:blue">AfterPublish<span style="color:black">"<span style="color:blue">
											<span style="color:red">AfterTargets<span style="color:blue">=<span style="color:black">"<span style="color:blue">GatherAllFilesToPublish<span style="color:black">"<span style="color:blue">&gt;<span style="color:black">
																	</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Consolas; font-size:9pt">    &lt;<span style="color:#a31515">Exec<span style="color:blue">
					<span style="color:red">Command<span style="color:blue">=<span style="color:black">"<span style="color:blue">npm run gulp -- after-publish --options --themes Theme1,Theme2 --projectFolder $(MSBuildProjectDirectory) --packageFolder $(_PackageTempDir) --publishFolder $(publishUrl)<span style="color:black">"<span style="color:blue"> /&gt;<span style="color:black">
											</span></span></span></span></span></span></span></span></span></span></p><p><span style="color:blue; font-family:Consolas; font-size:9pt">  &lt;/<span style="color:#a31515">Target<span style="color:blue">&gt;<span style="color:black">
					</span></span></span></span></p><p><span style="color:blue"><span style="font-family:Consolas; font-size:9pt">&lt;/<span style="color:#a31515">Project<span style="color:blue">&gt;</span></span></span><span style="font-family:Times New Roman; font-size:12pt"> </span></span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p> 
 </p><p> 
 </p><h3>Alter csproj 
</h3><p><span style="color:#333333; font-family:Helvetica; font-size:10pt">Add a "before build" step (just before the "project" end tag), to apply theming whenever the project is build (even in development) </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p><span style="color:blue; font-family:Courier New"><span style="font-size:9pt">&lt;<span style="color:#a31515">Target<span style="color:blue">
						<span style="color:red">Name<span style="color:blue">=<span style="color:black">"<span style="color:blue">BeforeBuild<span style="color:black">"<span style="color:blue">&gt;<span style="color:black">
												</span></span></span></span></span></span></span></span></span></span><span style="font-size:12pt">
			</span></span></p><p><span style="color:blue; font-family:Courier New"><span style="font-size:9pt">&lt;<span style="color:#a31515">Exec<span style="color:blue">
						<span style="color:red">Command<span style="color:blue">=<span style="color:black">"<span style="color:blue">npm run gulp -- apply-theming<span style="color:black">"<span style="color:blue"> /&gt;<span style="color:black">
												</span></span></span></span></span></span></span></span></span></span><span style="font-size:12pt">
			</span></span></p><p><span style="color:blue; font-family:Courier New"><span style="font-size:9pt">&lt;/<span style="color:#a31515">Target<span style="color:blue">&gt;<span style="color:black">
						</span></span></span></span><span style="font-size:12pt">
			</span></span></p><p><span style="color:blue; font-family:Courier New"><span style="font-size:9pt">&lt;/<span style="color:#a31515">Project<span style="color:blue">&gt;</span></span></span><span style="color:#333333; font-size:10pt">
			</span><span style="font-size:12pt">
			</span></span></p><p> 
 </p><p><span style="color:#333333; font-family:Helvetica; font-size:10pt">This will only run the theming and it will run the theming inside the current project folder. </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p> 
 </p><p> 
 </p><p> 
 </p><h3>Add or update package.json 
</h3><p><span style="color:#333333; font-family:Helvetica; font-size:10pt">After saving this file, Visual Studio will automatically run gulp install, to install all npm packages. </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p> 
 </p><p><span style="font-family:Courier New"><span style="color:black; font-size:9pt">{ </span><span style="font-size:12pt">
			</span></span></p><p><span style="color:black; font-family:Courier New"><span style="font-size:9pt">    <span style="color:#2e75b6">"version"<span style="color:black">: <span style="color:#a31515">"1.0.0"<span style="color:black">, </span></span></span></span></span><span style="font-size:12pt">
			</span></span></p><p><span style="color:black; font-family:Courier New"><span style="font-size:9pt">    <span style="color:#2e75b6">"name"<span style="color:black">: <span style="color:#a31515">"MyWebApp"<span style="color:black">, </span></span></span></span></span><span style="font-size:12pt">
			</span></span></p><p><span style="color:black; font-family:Courier New"><span style="font-size:9pt">    <span style="color:#2e75b6">"private"<span style="color:black">: <span style="color:blue">true<span style="color:black">, </span></span></span></span></span><span style="font-size:12pt">
			</span></span></p><p style="margin-left: 36pt"><span style="color:#2e75b6; font-family:Courier New"><span style="font-size:9pt">"devDependencies"<span style="color:black">: { </span></span><span style="font-size:12pt">
			</span></span></p><p style="margin-left: 36pt"><span style="color:#2e75b6; font-family:Courier New"><span style="font-size:9pt">"del"<span style="color:black">: <span style="color:#a31515">"&gt;=2.2.1"<span style="color:black">, </span></span></span></span><span style="font-size:12pt">
			</span></span></p><p style="margin-left: 36pt"><span style="color:#2e75b6; font-family:Courier New"><span style="font-size:9pt">"gulp"<span style="color:black">: <span style="color:#a31515">"&gt;=3.9.1"<span style="color:black">, </span></span></span></span><span style="font-size:12pt">
			</span></span></p><p style="margin-left: 36pt"><span style="color:#2e75b6; font-family:Courier New"><span style="font-size:9pt">"gulp-plumber"<span style="color:black">: <span style="color:#a31515">"&gt;=1.1.0"<span style="color:black">, </span></span></span></span><span style="font-size:12pt">
			</span></span></p><p style="margin-left: 36pt"><span style="color:#2e75b6; font-family:Courier New"><span style="font-size:9pt">"gulp-postcss"<span style="color:black">: <span style="color:#a31515">"&gt;=6.1.1"<span style="color:black">, </span></span></span></span><span style="font-size:12pt">
			</span></span></p><p style="margin-left: 36pt"><span style="color:#2e75b6; font-family:Courier New"><span style="font-size:9pt">"gulp-rename"<span style="color:black">: <span style="color:#a31515">"&gt;=1.2.2"<span style="color:black">, </span></span></span></span><span style="font-size:12pt">
			</span></span></p><p style="margin-left: 36pt"><span style="color:#2e75b6; font-family:Courier New"><span style="font-size:9pt">"gulp-util"<span style="color:black">: <span style="color:#a31515">"&gt;=3.0.7"<span style="color:black">, </span></span></span></span><span style="font-size:12pt">
			</span></span></p><p style="margin-left: 36pt"><span style="color:#2e75b6; font-family:Courier New"><span style="font-size:9pt">"postcss-import"<span style="color:black">: <span style="color:#a31515">"&gt;=8.1.2"<span style="color:black">, </span></span></span></span><span style="font-size:12pt">
			</span></span></p><p style="margin-left: 36pt"><span style="color:#2e75b6; font-family:Courier New"><span style="font-size:9pt">"postcss-cssnext"<span style="color:black">: <span style="color:#a31515">"&gt;=2.7.0"<span style="color:black">
						</span></span></span></span><span style="font-size:12pt">
			</span></span></p><p style="margin-left: 36pt"> 
 </p><p style="margin-left: 36pt"><span style="font-family:Courier New"><span style="color:black; font-size:9pt">}, </span><span style="font-size:12pt">
			</span></span></p><p style="margin-left: 36pt"><span style="color:#2e75b6; font-family:Courier New"><span style="font-size:9pt">"scripts"<span style="color:black">: { </span></span><span style="font-size:12pt">
			</span></span></p><p style="margin-left: 36pt"><span style="color:#2e75b6; font-family:Courier New"><span style="font-size:9pt">"gulp"<span style="color:black">: <span style="color:#a31515">"gulp"<span style="color:black">
						</span></span></span></span><span style="font-size:12pt">
			</span></span></p><p style="margin-left: 36pt"><span style="font-family:Courier New"><span style="color:black; font-size:9pt">} </span><span style="font-size:12pt">
			</span></span></p><p><span style="color:black; font-family:Courier New"><span style="font-size:9pt">}</span><span style="color:#333333; font-size:10pt">
			</span><span style="font-size:12pt">
			</span></span></p><p> 
 </p><p> 
 </p><p> 
 </p><p> 
 </p><h3>Add a gulpfile.js to the root of your web application 
</h3><p> 
 </p><p><span style="color:green; font-family:Courier New; font-size:9pt">/**
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> * The version of gulp and all it's dependencies are managed in the package.json file.
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> */<span style="color:black">
			</span></span></p><p><span style="color:#a31515; font-family:Courier New; font-size:9pt">'use strict'<span style="color:black">;
</span></span></p><p>
 </p><p><span style="color:green; font-family:Courier New; font-size:9pt">// Dependencies<span style="color:black">
			</span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">const<span style="color:black"> fs = require(<span style="color:#a31515">'fs'<span style="color:black">);
</span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">const<span style="color:black"> gulp = require(<span style="color:#a31515">'gulp'<span style="color:black">);
</span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">const<span style="color:black"> debug = require(<span style="color:#a31515">'gulp-debug'<span style="color:black">); <span style="color:green">// Can be used to log all files in a gulp stream (gulp.src or gulp.dest).<span style="color:black">
							</span></span></span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">const<span style="color:black"> jshint = require(<span style="color:#a31515">'gulp-jshint'<span style="color:black">);
</span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">const<span style="color:black"> livereload = require(<span style="color:#a31515">'gulp-livereload'<span style="color:black">);
</span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">const<span style="color:black"> plumber = require(<span style="color:#a31515">'gulp-plumber'<span style="color:black">);
</span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">const<span style="color:black"> util = require(<span style="color:#a31515">'gulp-util'<span style="color:black">);
</span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">const<span style="color:black"> path = require(<span style="color:#a31515">'path'<span style="color:black">);
</span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">const<span style="color:black"> helpers = require(<span style="color:#a31515">'./gulpfile-helpers.js'<span style="color:black">);
</span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">const<span style="color:black"> log = helpers.log;
</span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">const<span style="color:black"> defaultTheme = <span style="color:#a31515">'Theme1'<span style="color:black">;
</span></span></span></span></p><p>
 </p><p><span style="color:green; font-family:Courier New; font-size:9pt">/**
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> * The default task.
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> */<span style="color:black">
			</span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">gulp.task(<span style="color:#a31515">'default'<span style="color:black">, <span style="color:blue">function<span style="color:black"> () {
</span></span></span></span></span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">});
</span></p><p>
 </p><p><span style="color:green; font-family:Courier New; font-size:9pt">/**
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> * This task will be called from the "Deploy.pubxml".
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> */<span style="color:black">
			</span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">gulp.task(<span style="color:#a31515">"after-publish"<span style="color:black">, <span style="color:blue">function<span style="color:black"> () {
</span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">const<span style="color:black"> themes = (util.env.themes || <span style="color:#a31515">'Theme1,Theme2'<span style="color:black">).trim().split(<span style="color:#a31515">','<span style="color:black">);
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">const<span style="color:black"> projectFolder = (util.env.projectFolder || path.resolve(<span style="color:#a31515">'.'<span style="color:black">)).trim();
</span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">const<span style="color:black"> packageFolder = path.resolve((util.env.packageFolder || <span style="color:#a31515">"..\\bin\\Release\\Package\\PackageTmp"<span style="color:black">).trim());
</span></span></span></span></span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:green">// When this task is passed an environment variable "publishFolder", we expect the "publishFolder" to be the path to the first "themed release build".<span style="color:black">
				</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:green">// See the Deploy.pubxml for more explanation.<span style="color:black">
				</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">var<span style="color:black"> publishFolder = <span style="color:#a31515">"C:\\Release"<span style="color:black">;
</span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">if<span style="color:black">(util.env.publishFolder) {
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">        publishFolder = path.dirname(util.env.publishFolder.trim());
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    }
</span></p><p>    
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">    log(<span style="color:#a31515">`after-publish: themes - <span style="color:black">${themes}<span style="color:#a31515">`<span style="color:black">);
</span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    log(<span style="color:#a31515">`after-publish: projectFolder - <span style="color:black">${projectFolder}<span style="color:#a31515">`<span style="color:black">);
</span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    log(<span style="color:#a31515">`after-publish: packageFolder - <span style="color:black">${packageFolder}<span style="color:#a31515">`<span style="color:black">);
</span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    log(<span style="color:#a31515">`after-publish: publishFolder - <span style="color:black">${publishFolder}<span style="color:#a31515">`<span style="color:black">);
</span></span></span></span></span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:green">// Publish each theme.<span style="color:black">
				</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    themes.map((theme) =&gt; {
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">        helpers.publishTheme(theme.trim(), defaultTheme, projectFolder, packageFolder, publishFolder);
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    });
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">});
</span></p><p>
 </p><p><span style="color:green; font-family:Courier New; font-size:9pt">/**
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> * The "BeforeBuild" target in the " csproj" will call this gulp task.
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> *
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> * If you want to generate a theme other than the default theme, use the command line:
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> * npm run gulp -- apply-theming --options --theme Theme1
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> */<span style="color:black">
			</span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">gulp.task(<span style="color:#a31515">'apply-theming'<span style="color:black">, <span style="color:blue">function<span style="color:black"> () {
</span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">const<span style="color:black"> theme = (util.env.theme || defaultTheme);
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    helpers.applyTheme(theme, path.resolve(<span style="color:#a31515">'.'<span style="color:black">), path.resolve(<span style="color:#a31515">'.'<span style="color:black">));
</span></span></span></span></span></p><p><span style="font-family:Courier New"><span style="color:black; font-size:9pt">});</span><span style="font-size:12pt">
			</span></span></p><p> 
 </p><p> 
 </p><p> 
 </p><p> 
 </p><h3>Add a gulpfile.helper.js to the root of your web application 
</h3><p> 
 </p><p><span style="color:blue; font-family:Courier New; font-size:9pt">const<span style="color:black"> del = require(<span style="color:#a31515">'del'<span style="color:black">);
</span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">const<span style="color:black"> gulp = require(<span style="color:#a31515">'gulp'<span style="color:black">);
</span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">const<span style="color:black"> path = require(<span style="color:#a31515">'path'<span style="color:black">);
</span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">const<span style="color:black"> postcss = require(<span style="color:#a31515">'gulp-postcss'<span style="color:black">);
</span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">const<span style="color:black"> postcssImport = require(<span style="color:#a31515">'postcss-import'<span style="color:black">);
</span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">const<span style="color:black"> postcssNext = require(<span style="color:#a31515">'postcss-cssnext'<span style="color:black">);
</span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">const<span style="color:black"> rename = require(<span style="color:#a31515">'gulp-rename'<span style="color:black">);
</span></span></span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">const<span style="color:black"> util = require(<span style="color:#a31515">'gulp-util'<span style="color:black">);
</span></span></span></span></p><p>
 </p><p><span style="color:green; font-family:Courier New; font-size:9pt">/**
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> * Copy images and variables.cssn (cssnext) from the "theme" folder to the correct location.
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> * projectFolder = the folder containing the "*.csproj" file.
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> * destinationFolder = the folder where the theme files will be placed.
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> */<span style="color:black">
			</span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">function<span style="color:black"> applyTheme(theme, projectFolder, publishFolder) {
</span></span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:green">// Copy image files to publish folder.<span style="color:black">
				</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    copyImages(theme, projectFolder, publishFolder)
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    .on(<span style="color:#a31515">'finish'<span style="color:black">, runCopyCssNextThemeFiles);
</span></span></span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:green">// Copy css next theme files inside publish folder to the "App/Styles" folder.<span style="color:black">
				</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">function<span style="color:black"> runCopyCssNextThemeFiles() {
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">        copyCssNextThemeFiles(theme, publishFolder)
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">            .on(<span style="color:#a31515">'finish'<span style="color:black">, runGenerateCss);
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    }
</span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:green">// Generate css from css next files.<span style="color:black">
				</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">function<span style="color:black"> runGenerateCss() {
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">        generateCss(publishFolder);
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    }
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">}
</span></p><p>
 </p><p><span style="color:green; font-family:Courier New; font-size:9pt">/*
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> * Copy all css next files from the project folder to the specific theme publish folder.
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> */<span style="color:black">
			</span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">function<span style="color:black"> copyCssNextFiles(projectFolder, publishThemeFolder) {
</span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">const<span style="color:black"> src = path.join(projectFolder, <span style="color:#a31515">'/**/*.cssn'<span style="color:black">);
</span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">const<span style="color:black"> dest = publishThemeFolder;
</span></span></span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">    log(<span style="color:#a31515">`copyCssNextFiles: src - <span style="color:black">${src}<span style="color:#a31515">`<span style="color:black">);
</span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    log(<span style="color:#a31515">`copyCssNextFiles: dest - <span style="color:black">${dest}<span style="color:#a31515">`<span style="color:black">);
</span></span></span></span></span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">return<span style="color:black"> gulp.src(src)
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">        .pipe(gulp.dest(publishThemeFolder));
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">}
</span></p><p>
 </p><p><span style="color:green; font-family:Courier New; font-size:9pt">/**
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> * Copy theme css next files (including variables.cssn) from the "theme" folder to the "App/Styles" folder.
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> */<span style="color:black">
			</span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">function<span style="color:black"> copyCssNextThemeFiles(theme, publishFolder) {
</span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">const<span style="color:black"> src = path.join(publishFolder, <span style="color:#a31515">'Themes/'<span style="color:black"> + theme + <span style="color:#a31515">'/**/*.cssn'<span style="color:black">);
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">const<span style="color:black"> dest = path.join(publishFolder, <span style="color:#a31515">"App/Styles"<span style="color:black">);
</span></span></span></span></span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">    log(<span style="color:#a31515">`copyCssNextThemeFiles: src - <span style="color:black">${src}<span style="color:#a31515">`<span style="color:black">);
</span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    log(<span style="color:#a31515">`copyCssNextThemeFiles: dest - <span style="color:black">${dest}<span style="color:#a31515">`<span style="color:black">);
</span></span></span></span></span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">return<span style="color:black"> gulp.src(src)
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">        .pipe(gulp.dest(dest));
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">}
</span></p><p>
 </p><p><span style="color:blue; font-family:Courier New; font-size:9pt">function<span style="color:black"> copyImages(theme, projectFolder, destinationFolder) {
</span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">const<span style="color:black"> src = path.join(projectFolder, <span style="color:#a31515">'Themes/'<span style="color:black"> + theme + <span style="color:#a31515">'/Images/**/*.*'<span style="color:black">);
</span></span></span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">const<span style="color:black"> dest = path.join(destinationFolder, <span style="color:#a31515">'App/Images'<span style="color:black">);
</span></span></span></span></span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">    log(<span style="color:#a31515">`copyImages: src - <span style="color:black">${src}<span style="color:#a31515">`<span style="color:black">);
</span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    log(<span style="color:#a31515">`copyImages: dest - <span style="color:black">${dest}<span style="color:#a31515">`<span style="color:black">);
</span></span></span></span></span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">return<span style="color:black"> gulp.src(src)
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">            .pipe(gulp.dest(dest));
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">}
</span></p><p>
 </p><p><span style="color:green; font-family:Courier New; font-size:9pt">/*
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> * Copy all files from the Visual Studio package temp folder to the specific theme publish folder.
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> */<span style="color:black">
			</span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">function<span style="color:black"> copyPackageFiles(packageFiles, publishThemeFolder) {
</span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">const<span style="color:black"> src = packageFiles;
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">const<span style="color:black"> dest = publishThemeFolder;
</span></span></span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">    log(<span style="color:#a31515">`copyPackageFiles: src - <span style="color:black">${src}<span style="color:#a31515">`<span style="color:black">);
</span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    log(<span style="color:#a31515">`copyPackageFiles: dest - <span style="color:black">${dest}<span style="color:#a31515">`<span style="color:black">);
</span></span></span></span></span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">return<span style="color:black"> gulp.src(packageFiles)
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">        .pipe(gulp.dest(publishThemeFolder));
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">}
</span></p><p>
 </p><p><span style="color:green; font-family:Courier New; font-size:9pt">/**
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> * Compile cssn (cssnext) to css.
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> */<span style="color:black">
			</span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">function<span style="color:black"> generateCss(publishFolder) {
</span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">const<span style="color:black"> src = path.join(publishFolder, <span style="color:#a31515">'App/**/*.cssn'<span style="color:black">);
</span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">const<span style="color:black"> dest = path.join(publishFolder, <span style="color:#a31515">'App'<span style="color:black">);
</span></span></span></span></span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">    log(<span style="color:#a31515">`generateCss: src - <span style="color:black">${src}<span style="color:#a31515">`<span style="color:black">);
</span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    log(<span style="color:#a31515">`generateCss: dest - <span style="color:black">${dest}<span style="color:#a31515">`<span style="color:black">);
</span></span></span></span></span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">const<span style="color:black"> plugins = [
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">        postcssImport,
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">        postcssNext
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    ];
</span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">return<span style="color:black"> gulp.src(src)
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">            .pipe(postcss(plugins))
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">            .pipe(rename({
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">                extname: <span style="color:#a31515">".css"<span style="color:black">
				</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">            }))
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">            .on(<span style="color:#a31515">'error'<span style="color:black">, log)
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">            .pipe(gulp.dest(dest));
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">}
</span></p><p>
 </p><p><span style="color:green; font-family:Courier New; font-size:9pt">/**
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> * Log message or an array of messages.
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> */<span style="color:black">
			</span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">function<span style="color:black"> log(message) {
</span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">if<span style="color:black"> (Array.isArray(message)) {
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">for<span style="color:black"> (<span style="color:blue">var<span style="color:black"> i = 0, length = message.length; i &lt; length; i++) {
</span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">            util.log(message[i]);
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">        }
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    }
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">else<span style="color:black"> {
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">        util.log(message);
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    }
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">}
</span></p><p>
 </p><p><span style="color:blue; font-family:Courier New; font-size:9pt">function<span style="color:black"> publishTheme(theme, defaultTheme, projectFolder, packageFolder, publishFolder) {
</span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">const<span style="color:black"> publishThemeFolder = path.join(publishFolder, theme);
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">const<span style="color:black"> publishThemeFiles = path.join(publishThemeFolder, <span style="color:#a31515">"**"<span style="color:black">);
</span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">const<span style="color:black"> packageFiles = path.join(packageFolder, <span style="color:#a31515">'**/*'<span style="color:black">);
</span></span></span></span></span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">    log(<span style="color:#a31515">`publishTheme: publishThemeFolder - <span style="color:black">${publishThemeFolder}<span style="color:#a31515">`<span style="color:black">);
</span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    log(<span style="color:#a31515">`publishTheme: publishThemeFiles - <span style="color:black">${publishThemeFiles}<span style="color:#a31515">`<span style="color:black">);
</span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    log(<span style="color:#a31515">`publishTheme: packageFiles - <span style="color:black">${packageFiles}<span style="color:#a31515">`<span style="color:black">);
</span></span></span></span></span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:green">// Remove publish folder.<span style="color:black">
				</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    del.sync([publishThemeFiles], { force: <span style="color:blue">true<span style="color:black"> });
</span></span></span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:green">// Copy package files to publish folder.<span style="color:black">
				</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    copyPackageFiles(packageFiles, publishThemeFolder)
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">        .on(<span style="color:#a31515">'finish'<span style="color:black">, runCopyCssNextFiles);
</span></span></span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:green">// Copy css next files to publish folder.<span style="color:black">
				</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">function<span style="color:black"> runCopyCssNextFiles() {
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">        copyCssNextFiles(projectFolder, publishThemeFolder)
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">            .on(<span style="color:#a31515">'finish'<span style="color:black">, runCopyImages);
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    }
</span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">function<span style="color:black"> runCopyImages() {
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:green">// Copy image files to publish folder.<span style="color:black">
				</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">        copyImages(theme, projectFolder, publishThemeFolder)
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">        .on(<span style="color:#a31515">'finish'<span style="color:black">, runCopyCssNextThemeFiles);
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    }
</span></p><p>    
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:green">// Copy css next theme files inside publish folder to the "App/Styles" folder.<span style="color:black">
				</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">function<span style="color:black"> runCopyCssNextThemeFiles() {
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">        copyCssNextThemeFiles(theme, publishThemeFolder)
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">            .on(<span style="color:#a31515">'finish'<span style="color:black">, runGenerateCss);
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    }
</span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:green">// Generate css from css next files.<span style="color:black">
				</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">function<span style="color:black"> runGenerateCss() {
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">        generateCss(publishThemeFolder)
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">            .on(<span style="color:#a31515">'finish'<span style="color:black">, runDeleteCssNextFiles);
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    }
</span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:green">// Delete all css next files in the publish folder.<span style="color:black">
				</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">function<span style="color:black"> runDeleteCssNextFiles() {
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">
			<span style="color:blue">const<span style="color:black"> ccsNextFiles = path.join(publishThemeFolder, <span style="color:#a31515">'**/*.cssn'<span style="color:black">);
</span></span></span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">        log(<span style="color:#a31515">`runDeleteCssNextFiles: ccsNextFiles - <span style="color:black">${ccsNextFiles}<span style="color:#a31515">`<span style="color:black">);
</span></span></span></span></span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">        del.sync([ccsNextFiles], { force: <span style="color:blue">true<span style="color:black"> });
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    }
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">}
</span></p><p>
 </p><p><span style="color:green; font-family:Courier New; font-size:9pt">/**
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> * Log message to a log file, creating it, when it does not exist.
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> * The file will always be overwritten.
</span></p><p><span style="color:green; font-family:Courier New; font-size:9pt"> */<span style="color:black">
			</span></span></p><p><span style="color:blue; font-family:Courier New; font-size:9pt">function<span style="color:black"> writeToLogFile(message) {
</span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">    fs.writeFileSync(<span style="color:#a31515">'gulp.log.txt'<span style="color:black">, message);
</span></span></span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">}
</span></p><p>
 </p><p><span style="color:black; font-family:Courier New; font-size:9pt">exports.applyTheme = applyTheme;
</span></p><p><span style="color:black; font-family:Courier New; font-size:9pt">exports.log = log;
</span></p><p><span style="color:black; font-family:Courier New"><span style="font-size:9pt">exports.publishTheme = publishTheme;</span><span style="color:#333333; font-size:10pt">
			</span><span style="font-size:12pt">
			</span></span></p><p> 
 </p><p> 
 </p><h3>Alter the .gitignore file 
</h3><p> 
 </p><p><span style="color:black; font-family:Consolas; font-size:9pt">/App/Images/*.* </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">/App/Styles/variables.* </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p><span style="color:black; font-family:Consolas; font-size:9pt">/App/**/*.css </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p><span style="color:black"><span style="font-family:Consolas; font-size:9pt">!/App/Libraries/**/*.css</span><span style="color:#333333; font-family:Helvetica; font-size:10pt">
			</span><span style="font-family:Times New Roman; font-size:12pt">
			</span></span></p><p> 
 </p><p><span style="color:#333333; font-family:Helvetica; font-size:10pt">We excluded the copied "themed" images. </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p><span style="color:#333333; font-family:Helvetica; font-size:10pt">We excluded the copied "themed" variables.cssn. </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p><span style="color:#333333; font-family:Helvetica; font-size:10pt">We excluded all css, except the css in the libraries folder. </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p> 
 </p><p> 
 </p><p> 
 </p><p><span style="color:#333333; font-family:Helvetica; font-size:10pt">Now when you publish the project, the folder C:\Release\MyWebApp, should contain 2 "release builds" : Theme1 and Theme2. </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p><span style="color:#333333; font-family:Helvetica; font-size:10pt">Both containing the specific themed images and css. </span><span style="font-family:Times New Roman; font-size:12pt">
		</span></p><p><span style="font-family:Times New Roman; font-size:12pt"> </span> </p>
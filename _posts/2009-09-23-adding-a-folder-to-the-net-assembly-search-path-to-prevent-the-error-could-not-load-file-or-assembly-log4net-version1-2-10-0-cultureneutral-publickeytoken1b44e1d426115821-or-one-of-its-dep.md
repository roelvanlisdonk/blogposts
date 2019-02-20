---
ID: 713
post_title: 'Adding a folder to the .NET assembly search path, to prevent the error Could not load file or assembly &#039;log4net, Version=1.2.10.0, Culture=neutral, PublicKeyToken=1b44e1d426115821&#039; or one of its dependencies. The system cannot find the file specified.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/09/23/adding-a-folder-to-the-net-assembly-search-path-to-prevent-the-error-could-not-load-file-or-assembly-log4net-version1-2-10-0-cultureneutral-publickeytoken1b44e1d426115821-or-one-of-its-dep/
published: true
post_date: 2009-09-23 10:04:33
---
<p>   <br />If you use the <span style="color: #2b91af">XmlConfigurator</span>.Configure() . log4net function in a setup custom action to initialize the log4net logging, you can get the error:    <br />    <br /><strong>Could not load file or assembly 'log4net, Version=1.2.10.0, Culture=neutral, PublicKeyToken=1b44e1d426115821' or one of its dependencies. The system cannot find the file specified.      <br /></strong>    <br />This is because the msi package installs the assembly containing the custom action that uses the log4net assembly in a folder: C:\Program Files\MyCompany\MyProduct, but when the setup is started from a folder C:\Temp, the current working folder is <strong><font color="#000000">C:\Windows\SysWOW64</font></strong> on a x64 windows. The folder C:\Program Files\MyCompany\MyProduct is there for <font color="#ff0000">not included in the standard .NET assembly search path</font>. To add the folder C:\Program Files\MyCompany\MyProduct to the .NET assemlby search path use the following class:    <br />    <br />By the way this will also occur when you use custom configuration sections in you’re the App.config of you’re program (exe) and want to use the custom configuration sections during you’re msi installation with a custom setup action.</p>  <pre class="code"><span style="color: blue">public class </span><span style="color: #2b91af">AssemblyLoader
    </span>{
        <span style="color: blue">private string </span>_productInstallationFolder = <span style="color: blue">null</span>;
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Returns C:\Program Files\MyCompany\MyProduct or C:\Program Files (x86)\MyCompany\MyProduct depending on the platform.
        </span><span style="color: gray">/// &lt;/summary&gt;
        </span><span style="color: blue">public string </span>ProductInstallationFolder
        {
            <span style="color: blue">get
            </span>{
                <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(_productInstallationFolder))
                {
                    <span style="color: blue">var </span>programFilesFolder = System.<span style="color: #2b91af">Environment</span>.GetFolderPath(System.<span style="color: #2b91af">Environment</span>.<span style="color: #2b91af">SpecialFolder</span>.ProgramFiles);
                    _productInstallationFolder = <span style="color: #2b91af">Path</span>.Combine(programFilesFolder, <span style="color: #a31515">@&quot;MyCompany\MyProduct&quot;</span>);
                }
                <span style="color: blue">return </span>_productInstallationFolder;
            }
            <span style="color: blue">set
            </span>{
                _productInstallationFolder = <span style="color: blue">value</span>;
            }
        }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Add an evenhandler for adding a folder to the .NET assemlby search path.
        </span><span style="color: gray">/// &lt;/summary&gt;
        </span><span style="color: blue">public void </span>BindAssemblyResolveEventHandler()
        {
            <span style="color: blue">var </span>currentDomain = <span style="color: #2b91af">AppDomain</span>.CurrentDomain;
            currentDomain.AssemblyResolve += <span style="color: blue">this</span>.LoadAssemlbyFromProductInstallationFolder;
        }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">This function is called when the .NET runtime searches for an assemlby to load and can't find that assembly in the current search path.
        </span><span style="color: gray">/// </span><span style="color: green">The current search path includes &quot;bin folder application&quot;, the global assemlby cache, system32 folder etc.
        </span><span style="color: gray">///
        /// </span><span style="color: green">This function adds a folder to the current search path at runtime.
        </span><span style="color: gray">///
        /// </span><span style="color: green">An assembly can be a dll or exe, the ResolveEventArgs argument does not cotain this information.
        </span><span style="color: gray">/// </span><span style="color: green">The code will first check if a dll exist in the given folder, if found it loads the dll.
        </span><span style="color: gray">/// </span><span style="color: green">If the dll is not found, the code checks if an executable exists in the given folder, if found it loads the exe.
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;sender&quot;&gt;&lt;/param&gt;
        /// &lt;param name=&quot;args&quot;&gt;&lt;/param&gt;
        /// &lt;returns&gt;&lt;/returns&gt;
        </span><span style="color: blue">public </span><span style="color: #2b91af">Assembly </span>LoadAssemlbyFromProductInstallationFolder(<span style="color: blue">object </span>sender, <span style="color: #2b91af">ResolveEventArgs </span>args)
        {
            <span style="color: #2b91af">Assembly </span>result = <span style="color: blue">null</span>;
            <span style="color: blue">if </span>(args != <span style="color: blue">null </span>&amp;&amp; !<span style="color: blue">string</span>.IsNullOrEmpty(args.Name))
            {
                <span style="color: blue">var </span>folderPath = (<span style="color: blue">new </span><span style="color: #2b91af">FileInfo</span>(<span style="color: blue">this</span>.ProductInstallationFolder)).DirectoryName;
                <span style="color: blue">var </span>assemblyName = args.Name.Split(<span style="color: blue">new string</span>[] { <span style="color: #a31515">&quot;,&quot; </span>}, <span style="color: #2b91af">StringSplitOptions</span>.None)[0];
                <span style="color: blue">var </span>assemblyExtension = <span style="color: #a31515">&quot;dll&quot;</span>;
                <span style="color: blue">var </span>assemblyPath = <span style="color: #2b91af">Path</span>.Combine(folderPath, <span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;{0}.{1}&quot;</span>, assemblyName, assemblyExtension));
                <span style="color: blue">if </span>(!<span style="color: #2b91af">File</span>.Exists(assemblyPath))
                {
                    assemblyExtension = <span style="color: #a31515">&quot;exe&quot;</span>;
                    assemblyPath = <span style="color: #2b91af">Path</span>.Combine(folderPath, <span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;{0}.{1}&quot;</span>, assemblyName, assemblyExtension));
                }

                result = <span style="color: #2b91af">Assembly</span>.LoadFrom(assemblyPath);
            }

            <span style="color: blue">return </span>result;
        }
    }</pre>
<a href="http://11011.net/software/vspaste"></a>
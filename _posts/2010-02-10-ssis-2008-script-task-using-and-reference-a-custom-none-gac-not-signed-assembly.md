---
ID: 1019
post_title: >
  SSIS 2008 Script Task using and
  reference a custom none GAC (not signed)
  assembly
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/02/10/ssis-2008-script-task-using-and-reference-a-custom-none-gac-not-signed-assembly/
published: true
post_date: 2010-02-10 11:42:53
---
<p>&#160;</p>  <p>If you reference an custom none GAC assembly from you’re SSIS 2008 script task, you can get an exception, stating the assembly could not be found.</p>  <p><strong>Error</strong></p>  <p>Error: 0x1 at Filesysteem opschoning: System.Reflection.TargetInvocationException: Exception has been thrown by the target of an invocation. ---&gt; System.IO.FileNotFoundException: Could not load file or assembly 'Ada.Cdf, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null' or one of its dependencies. The system cannot find the file specified.   <br />File name: 'Ada.Cdf, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null'    <br />&#160;&#160; at ST_124cffcdeb3f407fa68f54b9192c0cdf.csproj.FileSystemCleaner.Clean()    <br />&#160;&#160; at ST_124cffcdeb3f407fa68f54b9192c0cdf.csproj.ScriptMain.Main() </p>  <p>WRN: Assembly binding logging is turned OFF.   <br />To enable assembly bind failure logging, set the registry value [HKLM\Software\Microsoft\Fusion!EnableLog] (DWORD) to 1.    <br />Note: There is some performance penalty associated with assembly bind failure logging.    <br />To turn this feature off, remove the registry value [HKLM\Software\Microsoft\Fusion!EnableLog]. </p>  <p>&#160;&#160; --- End of inner exception stack trace ---   <br />&#160;&#160; at System.RuntimeMethodHandle._InvokeMethodFast(Object target, Object[] arguments, SignatureStruct&amp; sig, MethodAttributes methodAttributes, RuntimeTypeHandle typeOwner)    <br />&#160;&#160; at System.RuntimeMethodHandle.InvokeMethodFast(Object target, Object[] arguments, Signature sig, MethodAttributes methodAttributes, RuntimeTypeHandle typeOwner)    <br />&#160;&#160; at System.Reflection.RuntimeMethodInfo.Invoke(Object obj, BindingFlags invokeAttr, Binder binder, Object[] parameters, CultureInfo culture, Boolean skipVisibilityChecks)    <br />&#160;&#160; at System.Reflection.RuntimeMethodInfo.Invoke(Object obj, BindingFlags invokeAttr, Binder binder, Object[] parameters, CultureInfo culture)    <br />&#160;&#160; at System.RuntimeType.InvokeMember(String name, BindingFlags bindingFlags, Binder binder, Object target, Object[] providedArgs, ParameterModifier[] modifiers, CultureInfo culture, String[] namedParams)    <br />&#160;&#160; at System.Type.InvokeMember(String name, BindingFlags invokeAttr, Binder binder, Object target, Object[] args, CultureInfo culture)    <br />&#160;&#160; at Microsoft.SqlServer.Dts.Tasks.ScriptTask.VSTATaskScriptingEngine.ExecuteScript()    <br />Task failed: Filesysteem opschoning    <br />Warning: 0x80019002 at OpschoonProces: SSIS Warning Code DTS_W_MAXIMUMERRORCOUNTREACHED.&#160; The Execution method succeeded, but the number of errors raised (1) reached the maximum allowed (1); resulting in failure. This occurs when the number of errors reaches the number specified in MaximumErrorCount. Change the MaximumErrorCount or fix the errors.    <br />SSIS package &quot;OpschoonProces.dtsx&quot; finished: Failure. </p>  <p>&#160;</p>  <p><strong>Solution</strong></p>  <p>To prevent this error, I use the AppDomain AssemblyResolve event to add a folder to the .NET assembly probing (search) path:   <br /></p>  <pre class="code"><span style="color: green">/*
   Microsoft SQL Server Integration Services Script Task
   Write scripts using Microsoft Visual C# 2008.
   The ScriptMain is the entry point class of the script.
*/

</span><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Data;
<span style="color: blue">using </span>Microsoft.SqlServer.Dts.Runtime;
<span style="color: blue">using </span>System.Windows.Forms;
<span style="color: blue">using </span>System.Reflection;
<span style="color: blue">using </span>System.IO;

<span style="color: blue">namespace </span>ST_124cffcdeb3f407fa68f54b9192c0cdf.csproj
{
    [System.AddIn.<span style="color: #2b91af">AddIn</span>(<span style="color: #a31515">&quot;ScriptMain&quot;</span>, Version = <span style="color: #a31515">&quot;1.0&quot;</span>, Publisher = <span style="color: #a31515">&quot;&quot;</span>, Description = <span style="color: #a31515">&quot;&quot;</span>)]
    <span style="color: blue">public partial class </span><span style="color: #2b91af">ScriptMain </span>: Microsoft.SqlServer.Dts.Tasks.ScriptTask.<span style="color: #2b91af">VSTARTScriptObjectModelBase
    </span>{

        <span style="color: blue">#region </span>VSTA generated code
        <span style="color: blue">enum </span><span style="color: #2b91af">ScriptResults
        </span>{
            Success = Microsoft.SqlServer.Dts.Runtime.<span style="color: #2b91af">DTSExecResult</span>.Success,
            Failure = Microsoft.SqlServer.Dts.Runtime.<span style="color: #2b91af">DTSExecResult</span>.Failure
        };
        <span style="color: blue">#endregion

        </span><span style="color: green">/*
        The execution engine calls this method when the task executes.
        To access the object model, use the Dts property. Connections, variables, events,
        and logging features are available as members of the Dts property as shown in the following examples.

        To reference a variable, call Dts.Variables[&quot;MyCaseSensitiveVariableName&quot;].Value;
        To post a log entry, call Dts.Log(&quot;This is my log text&quot;, 999, null);
        To fire an event, call Dts.Events.FireInformation(99, &quot;test&quot;, &quot;hit the help message&quot;, &quot;&quot;, 0, true);

        To use the connections collection use something like the following:
        ConnectionManager cm = Dts.Connections.Add(&quot;OLEDB&quot;);
        cm.ConnectionString = &quot;Data Source=localhost;Initial Catalog=AdventureWorks;Provider=SQLNCLI10;Integrated Security=SSPI;Auto Translate=False;&quot;;

        Before returning from this method, set the value of Dts.TaskResult to indicate success or failure.

        To open Help, press F1.
    */

        </span><span style="color: blue">public void </span>Main()
        {
            <span style="color: green">// Add bin folder to .NET assemlby search path
            </span><span style="color: blue">this</span>.BindAssemblyResolveEventHandler();

            <span style="color: #2b91af">FileSystemCleaner </span>cleaner = <span style="color: blue">new </span><span style="color: #2b91af">FileSystemCleaner</span>();
            cleaner.Clean();

            Dts.TaskResult = (<span style="color: blue">int</span>)<span style="color: #2b91af">ScriptResults</span>.Success;
        }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Add an evenhandler for adding a folder to the .NET assemlby search (probing) path.
        </span><span style="color: gray">/// &lt;/summary&gt;
        </span><span style="color: blue">public void </span>BindAssemblyResolveEventHandler()
        {
            <span style="color: blue">var </span>currentDomain = <span style="color: #2b91af">AppDomain</span>.CurrentDomain;
            currentDomain.AssemblyResolve += LoadAssemlbyFromProductInstallationFolder;
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
                <span style="color: blue">var </span>folderPath = GetExecutionPath();
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
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Get the current execution path
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;returns&gt;&lt;/returns&gt;
        </span><span style="color: blue">public string </span>GetExecutionPath()
        {
            <span style="color: blue">return new </span><span style="color: #2b91af">Uri</span>(System.IO.<span style="color: #2b91af">Path</span>.GetDirectoryName(<span style="color: #2b91af">Assembly</span>.GetExecutingAssembly().GetName().CodeBase)).LocalPath;
        }
    }
}</pre>
<a href="http://11011.net/software/vspaste"></a>
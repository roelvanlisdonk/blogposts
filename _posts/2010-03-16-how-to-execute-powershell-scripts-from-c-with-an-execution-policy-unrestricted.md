---
ID: 1129
post_title: 'How to execute PowerShell scripts from C# with an execution policy unrestricted'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/16/how-to-execute-powershell-scripts-from-c-with-an-execution-policy-unrestricted/
published: true
post_date: 2010-03-16 11:04:52
---
<p>When you are running a PowerShell script, you might get the error: </p>  <p>System.Management.Automation.PSSecurityException : File Test.ps1 cannot be loaded because the execution of scripts is disabled on this system. Please see &quot;get-help about_signing&quot; for more details.</p>  <p>&#160;</p>  <p><strong>Solution</strong></p>  <p>In development set the execution policy to Unrestricted.</p>  <p><strong>Set-ExecutionPolicy Unrestricted</strong></p>  <p><a title="http://www.itexperience.net/2008/07/18/file-cannot-be-loaded-because-the-execution-of-scripts-is-disabled-on-this-system-error-in-powershell/" href="http://www.itexperience.net/2008/07/18/file-cannot-be-loaded-because-the-execution-of-scripts-is-disabled-on-this-system-error-in-powershell/">http://www.itexperience.net/2008/07/18/file-cannot-be-loaded-because-the-execution-of-scripts-is-disabled-on-this-system-error-in-powershell/</a></p>  <p>&#160;</p>  <p><strong>PowerShell script (runs a function from an custom assembly)</strong></p>  <p>Param   <br />(    <br />&#160;&#160;&#160; [String]$Connection = &quot;&quot;,&#160;&#160;&#160;&#160; #The database connectionstring    <br />&#160;&#160;&#160; [String]$Folder = &quot;&quot;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; #The AppPool UserName    <br />)     <br />[System.Reflection.Assembly]::LoadWithPartialName(&quot;Ada.Cdf&quot;)    <br />$dd = new-object Ada.Cdf.Deployment.DatabaseDeployment    <br />$dd.ExecuteReCreatableScriptsInFolder($Connection, $Folder)</p>  <p>&#160;</p>  <p><strong>Unittest</strong></p>  <pre class="code">        [<span style="color: #2b91af">Test</span>]
        [<span style="color: #2b91af">Explicit</span>(<span style="color: #a31515">&quot;Not a unittest&quot;</span>)]
        <span style="color: blue">public void </span>RunExecuteReCreatableScriptsInFolder()
        {
            <span style="color: #2b91af">List</span>&lt;<span style="color: blue">string</span>&gt; parameters = <span style="color: blue">new </span><span style="color: #2b91af">List</span>&lt;<span style="color: blue">string</span>&gt;(){<span style="color: #a31515">@&quot;Data Source=.;Initial Catalog=TestDB;Integrated Security=SSPI;&quot;</span>, <span style="color: #a31515">@&quot;C:\Temp&quot;</span>};
            
            <span style="color: green">// Run a PowerShell script with two parameter and set execution policy to Unrestricted
            </span>RunPowershellScript(<span style="color: #a31515">@&quot;C:\Temp\Test.ps1&quot;</span>, parameters);
        }</pre>

<pre class="code"><strong>Function</strong>
        <span style="color: blue">private static void </span>RunPowershellScript(<span style="color: blue">string </span>scriptFile, <span style="color: #2b91af">List</span>&lt;<span style="color: blue">string</span>&gt; parameters)
        {
            <span style="color: green">// Validate parameters
            </span><span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(scriptFile)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;scriptFile&quot;</span>); }
            <span style="color: blue">if </span>(parameters == <span style="color: blue">null</span>) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;parameters&quot;</span>); }

            <span style="color: #2b91af">RunspaceConfiguration </span>runspaceConfiguration = <span style="color: #2b91af">RunspaceConfiguration</span>.Create();
            
            <span style="color: blue">using </span>(<span style="color: #2b91af">Runspace </span>runspace = <span style="color: #2b91af">RunspaceFactory</span>.CreateRunspace(runspaceConfiguration))
            {
                runspace.Open();
                <span style="color: #2b91af">RunspaceInvoke </span>scriptInvoker = <span style="color: blue">new </span><span style="color: #2b91af">RunspaceInvoke</span>(runspace);
                scriptInvoker.Invoke(<span style="color: #a31515">&quot;Set-ExecutionPolicy Unrestricted&quot;</span>);
                <span style="color: #2b91af">Pipeline </span>pipeline = runspace.CreatePipeline();
                <span style="color: #2b91af">Command </span>scriptCommand = <span style="color: blue">new </span><span style="color: #2b91af">Command</span>(scriptFile);
                <span style="color: #2b91af">Collection</span>&lt;<span style="color: #2b91af">CommandParameter</span>&gt; commandParameters = <span style="color: blue">new </span><span style="color: #2b91af">Collection</span>&lt;<span style="color: #2b91af">CommandParameter</span>&gt;();
                <span style="color: blue">foreach </span>(<span style="color: blue">string </span>scriptParameter <span style="color: blue">in </span>parameters)
                {
                    <span style="color: #2b91af">CommandParameter </span>commandParm = <span style="color: blue">new </span><span style="color: #2b91af">CommandParameter</span>(<span style="color: blue">null</span>, scriptParameter);
                    commandParameters.Add(commandParm);
                    scriptCommand.Parameters.Add(commandParm);
                }
                pipeline.Commands.Add(scriptCommand);
                <span style="color: #2b91af">Collection</span>&lt;<span style="color: #2b91af">PSObject</span>&gt; psObjects;
                psObjects = pipeline.Invoke();
            }
        } </pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p><a href="http://11011.net/software/vspaste">&#160;</a></p>
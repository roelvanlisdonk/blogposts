---
ID: 2305
post_title: 'How to: Adjust C# assembly probing path at runtime.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/12/19/how-to-adjust-c-assembly-probing-path-at-runtime/
published: true
post_date: 2011-12-19 13:21:40
---
<p>When a assembly is not found, when using the standard probing method, an assembly resolve event is fired, allowing to load the assembly from a different file system path:</p>  <p>&#160;</p>  <pre class="code"><span style="color: blue">public void </span>Test()
{
    <span style="color: #2b91af">AppDomain </span>currentDomain = <span style="color: #2b91af">AppDomain</span>.CurrentDomain;
    currentDomain.AssemblyResolve += <span style="color: blue">new </span><span style="color: #2b91af">ResolveEventHandler</span>(LoadFromSameFolder);
}
<span style="color: blue">public static </span><span style="color: #2b91af">Assembly </span>LoadFromSameFolder(<span style="color: blue">object </span>sender, <span style="color: #2b91af">ResolveEventArgs </span>args)
{
    <span style="color: blue">string </span>folderPath = <span style="color: #2b91af">Path</span>.GetDirectoryName(<span style="color: #2b91af">Assembly</span>.GetExecutingAssembly().Location);
    <span style="color: blue">string </span>assemblyPath = <span style="color: #2b91af">Path</span>.Combine(folderPath, <span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;{0}.dll&quot;</span>, <span style="color: blue">new </span><span style="color: #2b91af">AssemblyName</span>(args.Name).Name));
    <span style="color: blue">if </span>(!<span style="color: #2b91af">File</span>.Exists(assemblyPath))
    {
        assemblyPath = <span style="color: #2b91af">Path</span>.Combine(folderPath, <span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;{0}.exe&quot;</span>, <span style="color: blue">new </span><span style="color: #2b91af">AssemblyName</span>(args.Name).Name));
        <span style="color: blue">if </span>(!<span style="color: #2b91af">File</span>.Exists(assemblyPath))
        {
            <span style="color: blue">return null</span>;
        }
    }
    <span style="color: #2b91af">Assembly </span>assembly = <span style="color: #2b91af">Assembly</span>.LoadFrom(assemblyPath);
    <span style="color: blue">return </span>assembly;
}</pre>
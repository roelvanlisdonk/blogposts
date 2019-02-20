---
ID: 1802
post_title: 'Redirecting the Microsoft Visual Studio [devenv.exe] output during build from C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/11/05/redirecting-the-microsoft-visual-studio-devenv-exe-output-during-build-from-c/
published: true
post_date: 2010-11-05 14:33:34
---
<p>If you want to build a Microsoft Visual Studio solution file and show the output during build, you can use the following code:</p>  <p>&#160;</p>  <pre class="code"><span style="color: gray">/// &lt;summary&gt;
/// </span><span style="color: green">Rebuilds the Microsoft Visual Studio Solution in the given configuration.
</span><span style="color: gray">///     </span><span style="color: green">- Shows build output during build
</span><span style="color: gray">/// &lt;/summary&gt;
</span><span style="color: blue">public void </span>Rebuild()
{
    <span style="color: blue">string </span>logFilePath = <span style="color: #a31515">&quot;build.log&quot;</span>;
    <span style="color: blue">using </span>(<span style="color: #2b91af">Process </span>process = <span style="color: #2b91af">Process</span>.Start(
        <span style="color: #a31515">@&quot;C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\devenv.exe&quot;</span>, 
        <span style="color: blue">string</span>.Format(<span style="color: #a31515">@&quot;&quot;&quot;{0}&quot;&quot; /Rebuild Release /out {1}&quot;</span>, <span style="color: #a31515">@&quot;C:\Projects\Main.sln&quot;</span>, logFilePath)))
    {
        <span style="color: blue">using </span>(<span style="color: #2b91af">FileStream </span>fs = <span style="color: blue">new </span><span style="color: #2b91af">FileStream</span>(  logFilePath, 
                                                <span style="color: #2b91af">FileMode</span>.Open, 
                                                <span style="color: #2b91af">FileAccess</span>.Read, 
                                                <span style="color: #2b91af">FileShare</span>.ReadWrite))
        {
            <span style="color: blue">using </span>(<span style="color: #2b91af">StreamReader </span>sr = <span style="color: blue">new </span><span style="color: #2b91af">StreamReader</span>(fs))
            {
                <span style="color: blue">while </span>(!process.HasExited)
                {
                    <span style="color: blue">while </span>(!sr.EndOfStream)
                    {
                        <span style="color: #2b91af">Console</span>.WriteLine(sr.ReadLine());
                    }
                    <span style="color: #2b91af">Thread</span>.Sleep(1000);
                }
            }
        }
    }
    <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: #a31515">&quot;Rebuild completed&quot;</span>);
}</pre>
<a href="http://11011.net/software/vspaste"></a><a href="http://11011.net/software/vspaste"></a>
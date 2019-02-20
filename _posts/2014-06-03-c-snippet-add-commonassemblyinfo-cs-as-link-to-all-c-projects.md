---
ID: 3805
post_title: 'C# snippet: Add CommonAssemblyInfo.cs as link to all C# projects.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/06/03/c-snippet-add-commonassemblyinfo-cs-as-link-to-all-c-projects/
published: true
post_date: 2014-06-03 14:31:08
---
<p>We use a CommonAssemblyInfo.cs file, to contain all common AssemblyInfo information for all projects.</p>  <p>Like: </p>  <pre class="code"><span style="background: white; color: black">[</span><span style="background: white; color: blue">assembly</span><span style="background: white; color: black">: </span><span style="background: white; color: #2b91af">AssemblyVersion</span><span style="background: white; color: black">(</span><span style="background: white; color: #a31515">&quot;0.0.0.0&quot;</span><span style="background: white; color: black">)]
[</span><span style="background: white; color: blue">assembly</span><span style="background: white; color: black">: </span><span style="background: white; color: #2b91af">AssemblyFileVersion</span><span style="background: white; color: black">(</span><span style="background: white; color: #a31515">&quot;0.0.0.0&quot;</span><span style="background: white; color: black">)]
[</span><span style="background: white; color: blue">assembly</span><span style="background: white; color: black">: </span><span style="background: white; color: #2b91af">AssemblyCompanyAttribute</span><span style="background: white; color: black">(</span><span style="background: white; color: #a31515">&quot;ADA ICT&quot;</span><span style="background: white; color: black">)]
[</span><span style="background: white; color: blue">assembly</span><span style="background: white; color: black">: </span><span style="background: white; color: #2b91af">AssemblyCopyrightAttribute</span><span style="background: white; color: black">(</span><span style="background: white; color: #a31515">&quot;Copyright © ADA ICT 2014&quot;</span><span style="background: white; color: black">)]</span></pre>


<p>Our continuous integration system, alters the CommonAssemblyInfo.cs file add build time, to sync the TFS build version with the assemblies found in the solution.</p>

<p>&#160;</p>

<p>When you add this CommonAssemblyInfo.cs file as a link to your project in Microsoft Visual Studio:</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/06/image.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/06/image_thumb.png" width="580" height="345" /></a></p>

<p>&#160;</p>

<p>Microsoft Visual Studio, will merge the information in the AssemblyInfo.cs with the information in the CommonAssemblyInfo.cs.</p>

<p>&#160;</p>

<p>If you don’t want to add this link manual, you can use the following C# code:</p>

<p>&#160;</p>

<p><strong>VsSolution.cs</strong></p>

<pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">Research.Core.CodeGeneration
{
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Collections.Generic;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Linq;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Text;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Text.RegularExpressions;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Threading.Tasks;

</span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">VsSolution
</span><span style="background: white; color: black">{
</span><span style="background: white; color: gray">/// &lt;summary&gt;
/// </span><span style="background: white; color: green">Add CommonAssemblyInfo as link to a project.
</span><span style="background: white; color: gray">/// &lt;/summary&gt;
</span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">AddCommonAssemblyInfo(</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">content)
{
    </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">result = </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Empty;

    </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(!</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.IsNullOrWhiteSpace(content))
    {
        result = content;

        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">findRegEx = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Regex</span><span style="background: white; color: black">(</span><span style="background: white; color: #a31515">@&quot;&lt;ItemGroup&gt;.*
&lt;Compile Include=&quot;&quot;..\\SharedSource\\CommonAssemblyInfo.cs&quot;&quot;&gt;
&lt;Link&gt;CommonAssemblyInfo.cs&lt;/Link&gt;
&lt;/Compile&gt;.*
&lt;/ItemGroup&gt;&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #2b91af">RegexOptions</span><span style="background: white; color: black">.Singleline);

        </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(!findRegEx.IsMatch(content))
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">replaceRegEx = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Regex</span><span style="background: white; color: black">(</span><span style="background: white; color: #a31515">@&quot;&lt;ItemGroup&gt;&quot;</span><span style="background: white; color: black">);

            result = replaceRegEx.Replace(result, </span><span style="background: white; color: #a31515">@&quot;&lt;ItemGroup&gt;
&lt;Compile Include=&quot;&quot;..\\SharedSource\\CommonAssemblyInfo.cs&quot;&quot;&gt;
&lt;Link&gt;CommonAssemblyInfo.cs&lt;/Link&gt;
&lt;/Compile&gt;&quot;</span><span style="background: white; color: black">, 1);
        }

                
    }

    </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">result;
}

</span><span style="background: white; color: black">}
}
</span></pre>


<p>This code can be used with a small helper class to change all *.csproj files on disk:</p>

<p>&#160;</p>

<p><strong>FileSystem.cs</strong></p>

<pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">Research.Core.Components
{
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Collections.Generic;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.IO;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Threading.Tasks;
        
</span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">FileSystem
</span><span style="background: white; color: black">{
</span><span style="background: white; color: blue">public async </span><span style="background: white; color: #2b91af">Task </span><span style="background: white; color: black">FindAndReplace(</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">path, </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">searchPattern, </span><span style="background: white; color: #2b91af">SearchOption </span><span style="background: white; color: black">searchOption, 
    </span><span style="background: white; color: #2b91af">Func</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt; updateContent)
{
    </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">[] files = </span><span style="background: white; color: blue">await </span><span style="background: white; color: black">GetFilesAsync(path, searchPattern, searchOption);
    </span><span style="background: white; color: blue">foreach </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">file </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">files)
    {
        </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">content = </span><span style="background: white; color: blue">await </span><span style="background: white; color: black">ReadAllTextAsync(file);
        content = updateContent(content);
        </span><span style="background: white; color: blue">await </span><span style="background: white; color: black">WriteAllTextAsync(file, content);
    }
}

</span><span style="background: white; color: blue">public async </span><span style="background: white; color: #2b91af">Task</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">[]&gt; GetFilesAsync(</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">path, </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">searchPattern, </span><span style="background: white; color: #2b91af">SearchOption </span><span style="background: white; color: black">searchOption)
{
    </span><span style="background: white; color: blue">return await </span><span style="background: white; color: #2b91af">Task</span><span style="background: white; color: black">.Factory.StartNew(() =&gt;
    {
        </span><span style="background: white; color: blue">return </span><span style="background: white; color: #2b91af">Directory</span><span style="background: white; color: black">.GetFiles(path, searchPattern, searchOption);
    });
}

</span><span style="background: white; color: blue">public async </span><span style="background: white; color: #2b91af">Task</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt; ReadAllTextAsync(</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">path)
{
    </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">result = </span><span style="background: white; color: blue">await </span><span style="background: white; color: #2b91af">Task</span><span style="background: white; color: black">.Factory.StartNew(() =&gt; { </span><span style="background: white; color: blue">return </span><span style="background: white; color: #2b91af">File</span><span style="background: white; color: black">.ReadAllText(path); });
    </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">result;
}

</span><span style="background: white; color: blue">public async </span><span style="background: white; color: #2b91af">Task </span><span style="background: white; color: black">WriteAllTextAsync(</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">path, </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">content)
{
    </span><span style="background: white; color: blue">await </span><span style="background: white; color: #2b91af">Task</span><span style="background: white; color: black">.Factory.StartNew(() =&gt; { </span><span style="background: white; color: #2b91af">File</span><span style="background: white; color: black">.WriteAllText(path, content); });
}
}

</span><span style="background: white; color: black">}</span></pre>


<p>To execute the code use:</p>

<pre class="code"><p><span style="background: white; color: black">[</span><span style="background: white; color: #2b91af">TestMethod</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">FindAndReplace_should_replace_common_assemblyinfo()
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">solution = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">VsSolution</span><span style="background: white; color: black">();
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">fs = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">FileSystem</span><span style="background: white; color: black">();
            </span><span style="background: white; color: #2b91af">Task </span><span style="background: white; color: black">task = fs.FindAndReplace(</span><span style="background: white; color: #a31515">@&quot;C:\Projects\TNT\RouteMaker\Main-v1.0\Source&quot;</span><span style="background: white; color: black">, </span></p><p><span style="background: white; color: black"></span><span style="background: white; color: #a31515">&quot;AssemblyInfo.cs&quot;</span><span style="background: white; color: black">, System.IO.</span><span style="background: white; color: #2b91af">SearchOption</span><span style="background: white; color: black">.AllDirectories, solution.RemoveCommonAssemblyInfo);
            
            task.Wait();
        }</span></p></pre>


<p>Code can be found at:</p>

<p><a title="https://github.com/roelvanlisdonk/Research" href="https://github.com/roelvanlisdonk/Research">https://github.com/roelvanlisdonk/Research</a></p>
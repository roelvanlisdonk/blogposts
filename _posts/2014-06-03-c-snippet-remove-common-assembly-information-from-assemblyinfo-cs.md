---
ID: 3800
post_title: 'C# snippet: remove common assembly information from AssemblyInfo.cs'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/06/03/c-snippet-remove-common-assembly-information-from-assemblyinfo-cs/
published: true
post_date: 2014-06-03 11:12:48
---
<p>A C# method that I used to remove common assembly information from a AssemblyInfo.cs.</p>  <p>This method was used with a small FileSystem.cs class.</p>  <p>&#160;</p>  <pre class="code"><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">Remove common assembly info from the given content.
        </span><span style="background: white; color: gray">/// </span><span style="background: white; color: green">Like:
        </span><span style="background: white; color: gray">/// </span><span style="background: white; color: green">- AssemblyCompany
        </span><span style="background: white; color: gray">/// </span><span style="background: white; color: green">- AssemblyCopyright
        </span><span style="background: white; color: gray">/// </span><span style="background: white; color: green">- AssemblyVersion
        </span><span style="background: white; color: gray">/// </span><span style="background: white; color: green">- AssemblyFileVersion
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">RemoveCommonAssemblyInfo(</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">content)
        {
            </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">result = </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Empty;

            </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(!</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.IsNullOrWhiteSpace(content))
            {
                result = content;
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">regexes = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">Regex</span><span style="background: white; color: black">&gt;();
                regexes.Add(</span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Regex</span><span style="background: white; color: black">(</span><span style="background: white; color: #a31515">@&quot;\r\n\[assembly: AssemblyCompany\(&quot;&quot;{1}.*&quot;&quot;{1}\)]&quot;</span><span style="background: white; color: black">));
                regexes.Add(</span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Regex</span><span style="background: white; color: black">(</span><span style="background: white; color: #a31515">@&quot;\r\n\[assembly: AssemblyCopyright\(&quot;&quot;{1}.*&quot;&quot;{1}\)]&quot;</span><span style="background: white; color: black">));
                regexes.Add(</span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Regex</span><span style="background: white; color: black">(</span><span style="background: white; color: #a31515">@&quot;\r\n\[assembly: AssemblyVersion\(&quot;&quot;{1}.*&quot;&quot;{1}\)]&quot;</span><span style="background: white; color: black">));
                regexes.Add(</span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Regex</span><span style="background: white; color: black">(</span><span style="background: white; color: #a31515">@&quot;\r\n\[assembly: AssemblyFileVersion\(&quot;&quot;{1}.*&quot;&quot;{1}\)]&quot;</span><span style="background: white; color: black">));
                regexes.Add(</span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Regex</span><span style="background: white; color: black">(</span><span style="background: white; color: #a31515">@&quot;\r\n\r\n// Version information.*&quot;&quot;{1}\)]&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #2b91af">RegexOptions</span><span style="background: white; color: black">.Singleline));

                regexes.ForEach(x =&gt;
                {
                    result = x.Replace(result, </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Empty);
                });
            }

            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">result;
        }</span></pre>



<pre class="code"><p><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">Research.Core.Components
{
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Collections.Generic;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.IO;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Threading.Tasks;
        
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">FileSystem
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">public async </span><span style="background: white; color: #2b91af">Task </span><span style="background: white; color: black">FindAndReplace(</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">path, </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">searchPattern, </span><span style="background: white; color: #2b91af">SearchOption </span><span style="background: white; color: black">searchOption, </span></p><p><span style="background: white; color: black"></span><span style="background: white; color: #2b91af">Func</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt; updateContent)
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

    </span><span style="background: white; color: black">}</span></p></pre>


<p>&#160;</p>

<p>To replace all common assembly info found in all AssemblyInfo.cs files in a folder, use the code:</p>

<p>&#160;</p>

<pre class="code"><p><span style="background: white; color: blue">var </span><span style="background: white; color: black">solution = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">VsSolution</span><span style="background: white; color: black">();
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">fs = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">FileSystem</span><span style="background: white; color: black">();
            </span><span style="background: white; color: #2b91af">Task </span><span style="background: white; color: black">task = fs.FindAndReplace(</span><span style="background: white; color: #a31515">@&quot;C:\Projects\Github\roelvanlisdonk\Research\Main&quot;</span><span style="background: white; color: black">, </span></p><p><span style="background: white; color: black"></span><span style="background: white; color: #a31515">&quot;AssemblyInfo.cs&quot;</span><span style="background: white; color: black">, System.IO.</span><span style="background: white; color: #2b91af">SearchOption</span><span style="background: white; color: black">.AllDirectories, solution.RemoveCommonAssemblyInfo);
            task.Wait();</span></p></pre>


<p>&#160;</p>

<p>Code can be found at: <a title="https://github.com/roelvanlisdonk/Research" href="https://github.com/roelvanlisdonk/Research">https://github.com/roelvanlisdonk/Research</a></p>
---
ID: 3192
post_title: 'How to convert a JSON string, containing UTC datetime to a local server datetime string in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/04/10/how-to-convert-a-json-string-containing-utc-datetime-to-a-local-server-datetime-string-in-c/
published: true
post_date: 2013-04-10 17:11:06
---
<pre class="code"><span style="background: white; color: blue">using </span><span style="background: white; color: black">Microsoft.VisualStudio.TestTools.UnitTesting;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Newtonsoft.Json;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Collections.Generic;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Diagnostics;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.IO;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Text.RegularExpressions;

</span><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">Research.Rli.Tests
{
    [</span><span style="background: white; color: #2b91af">TestClass</span><span style="background: white; color: black">]
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">ResearchTester
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: black">
        [</span><span style="background: white; color: #2b91af">TestMethod</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Test()
        {
            </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">json = </span><span style="background: white; color: #a31515">@&quot;{&quot;&quot;date&quot;&quot;:&quot;&quot;2013-04-10T14:52:43.207Z&quot;&quot;}&quot;</span><span style="background: white; color: black">;
            </span><span style="background: white; color: #2b91af">Dto </span><span style="background: white; color: black">dto = </span><span style="background: white; color: #2b91af">JsonConvert</span><span style="background: white; color: black">.DeserializeObject&lt;</span><span style="background: white; color: #2b91af">Dto</span><span style="background: white; color: black">&gt;(json);
            </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">localTime = dto.date.ToLocalTime().ToString();
            </span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">.AreEqual(</span><span style="background: white; color: #a31515">&quot;10-4-2013 16:52:43&quot;</span><span style="background: white; color: black">, localTime); </span><span style="background: white; color: green">// In the Netherlands this test will succeed.
        </span><span style="background: white; color: black">}
    }
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">Dto
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">public </span><span style="background: white; color: #2b91af">DateTime </span><span style="background: white; color: black">date { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
    }
}</span></pre>


<pre class="code"><p>&#160;</p><p>&#160;</p><p>&#160;</p></pre>
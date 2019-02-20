---
ID: 3344
post_title: 'Dictionary lookup vs switch vs if performance in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/08/28/dictionairy-lookup-vs-switch-vs-if-performance-in-c/
published: true
post_date: 2013-08-28 15:09:46
---
<p>Lets say you want to execute a specific logging function based on a log level. Amongst others you could use a switch- or if statements or use a generic dictionary containing the functions to call.</p>  <p>&#160;</p>  <p>In mine code the generic dictionary has the advantage of being more testable, so I wanted to figure out what the performance impact of this dictionary lookup was. So I wrote a little test.</p>  <p>Each test will execute a log function 1 million times.</p>  <p>&#160;</p>  <p>&#160;</p>  <p><strong>Executing 1.000.000 times:</strong></p>  <p>Switch: <font color="#151515"><strong>374ms</strong></font></p>  <p>If: <strong>387ms </strong>(<font color="#ff0000">3% slower</font>)</p>  <p>Dictionary: <strong>393ms</strong> (<font color="#ff0000">5% slower</font>)</p>  <p>&#160;</p>  <p>&#160;</p>  <p>In my case this was enough to convince me to use the generic dictionary lookup for better testability.</p>  <p>&#160;</p>  <pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">PTB.Cs.Test.Research
{
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Collections.Generic;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.IO;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Xunit;

</span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">RliTester
</span><span style="background: white; color: black">{
    </span><span style="background: white; color: blue">private string </span><span style="background: white; color: black">_message;

    </span><span style="background: white; color: blue">private readonly </span><span style="background: white; color: #2b91af">Dictionary</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">Levels</span><span style="background: white; color: black">, </span><span style="background: white; color: #2b91af">Action</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt;&gt; _logFunctions;
    </span><span style="background: white; color: blue">public </span><span style="background: white; color: black">RliTester()
    {
        _logFunctions = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Dictionary</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">Levels</span><span style="background: white; color: black">, </span><span style="background: white; color: #2b91af">Action</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt;&gt;
        {
            { </span><span style="background: white; color: #2b91af">Levels</span><span style="background: white; color: black">.Debug, Debug },
            { </span><span style="background: white; color: #2b91af">Levels</span><span style="background: white; color: black">.Error, Error },
            { </span><span style="background: white; color: #2b91af">Levels</span><span style="background: white; color: black">.Info, Info },
            { </span><span style="background: white; color: #2b91af">Levels</span><span style="background: white; color: black">.Warning, Warning },
        };    
    }

    </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Debug(</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">message)
    {
        _message = message;
    }

    </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Error(</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">message)
    {
        _message = message;
    }

    </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Info(</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">message)
    {
        _message = message;
    }

    </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Warning(</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">message)
    {
        _message = message;
    }

    </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">ExecuteFunctionBySwitch(</span><span style="background: white; color: #2b91af">Levels </span><span style="background: white; color: black">level, </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">message)
    {
        </span><span style="background: white; color: blue">switch </span><span style="background: white; color: black">(level)
        {
            </span><span style="background: white; color: blue">case </span><span style="background: white; color: #2b91af">Levels</span><span style="background: white; color: black">.Debug:
                Debug(message);
                </span><span style="background: white; color: blue">break</span><span style="background: white; color: black">;
            </span><span style="background: white; color: blue">case </span><span style="background: white; color: #2b91af">Levels</span><span style="background: white; color: black">.Error:
                Error(message);
                </span><span style="background: white; color: blue">break</span><span style="background: white; color: black">;
            </span><span style="background: white; color: blue">case </span><span style="background: white; color: #2b91af">Levels</span><span style="background: white; color: black">.Info:
                Info(message);
                </span><span style="background: white; color: blue">break</span><span style="background: white; color: black">;
            </span><span style="background: white; color: blue">case </span><span style="background: white; color: #2b91af">Levels</span><span style="background: white; color: black">.Warning:
                Warning(message);
                </span><span style="background: white; color: blue">break</span><span style="background: white; color: black">;
        }
    }

    </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">ExecuteFunctionByIf(</span><span style="background: white; color: #2b91af">Levels </span><span style="background: white; color: black">level, </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">message)
    {
        </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(level == </span><span style="background: white; color: #2b91af">Levels</span><span style="background: white; color: black">.Debug)
        {
            Debug(message);
        }

        </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(level == </span><span style="background: white; color: #2b91af">Levels</span><span style="background: white; color: black">.Error)
        {
            Error(message);
        }

        </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(level == </span><span style="background: white; color: #2b91af">Levels</span><span style="background: white; color: black">.Info)
        {
            Info(message);
        }

        </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(level == </span><span style="background: white; color: #2b91af">Levels</span><span style="background: white; color: black">.Warning)
        {
            Warning(message);
        }
    }


    </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">ExecuteFunctionByDictionairyLookup(</span><span style="background: white; color: #2b91af">Levels </span><span style="background: white; color: black">level, </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">message)
    {
        _logFunctions[level].Invoke(message);
    }

    [</span><span style="background: white; color: #2b91af">Fact</span><span style="background: white; color: black">]
    </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Test_performance_ExecuteFunctionBySwitch()
    {
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">watch = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">System.Diagnostics.</span><span style="background: white; color: #2b91af">Stopwatch</span><span style="background: white; color: black">();
        watch.Start();

        </span><span style="background: white; color: blue">for</span><span style="background: white; color: black">(</span><span style="background: white; color: blue">int </span><span style="background: white; color: black">i = 0; i &lt; 1000000; i++)
        {
            ExecuteFunctionBySwitch(</span><span style="background: white; color: #2b91af">Levels</span><span style="background: white; color: black">.Info, </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">&quot;This is info message [{0}].&quot;</span><span style="background: white; color: black">, i));
        }

        watch.Stop();
        System.</span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine(watch.Elapsed.TotalMilliseconds);

        </span><span style="background: white; color: green">// Result: 374ms
    </span><span style="background: white; color: black">}

    [</span><span style="background: white; color: #2b91af">Fact</span><span style="background: white; color: black">]
    </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Test_performance_ExecuteFunctionIf()
    {
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">watch = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">System.Diagnostics.</span><span style="background: white; color: #2b91af">Stopwatch</span><span style="background: white; color: black">();
        watch.Start();
            
        </span><span style="background: white; color: blue">for </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">int </span><span style="background: white; color: black">i = 0; i &lt; 1000000; i++)
        {
            ExecuteFunctionByIf(</span><span style="background: white; color: #2b91af">Levels</span><span style="background: white; color: black">.Info, </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">&quot;This is info message [{0}].&quot;</span><span style="background: white; color: black">, i));
        }

        watch.Stop();
        System.</span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine(watch.Elapsed.TotalMilliseconds);

        </span><span style="background: white; color: green">// Result: 387ms
    </span><span style="background: white; color: black">}

    [</span><span style="background: white; color: #2b91af">Fact</span><span style="background: white; color: black">]
    </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Test_performance_ExecuteFunctionByDictionairyLookup()
    {
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">watch = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">System.Diagnostics.</span><span style="background: white; color: #2b91af">Stopwatch</span><span style="background: white; color: black">();
        watch.Start();

        </span><span style="background: white; color: blue">for </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">int </span><span style="background: white; color: black">i = 0; i &lt; 1000000; i++)
        {
            ExecuteFunctionByDictionairyLookup(</span><span style="background: white; color: #2b91af">Levels</span><span style="background: white; color: black">.Info, </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">&quot;This is info message [{0}].&quot;</span><span style="background: white; color: black">, i));
        }

        watch.Stop();
        System.</span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine(watch.Elapsed.TotalMilliseconds);

        </span><span style="background: white; color: green">// Result: 393ms
    </span><span style="background: white; color: black">}

        
}

</span><span style="background: white; color: gray">/// &lt;summary&gt;
/// </span><span style="background: white; color: green">Determines the level of the logging.
</span><span style="background: white; color: gray">/// &lt;/summary&gt;
</span><span style="background: white; color: blue">public enum </span><span style="background: white; color: #2b91af">Levels
</span><span style="background: white; color: black">{
    Error = 1,
    Warning = 2,
    Info = 3,
    Debug = 4
}
}

</span></pre>
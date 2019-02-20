---
ID: 3790
post_title: 'Dynamically call C# instance method by &quot;string&quot; name, without performance overhead.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/05/23/dynamically-call-c-instance-method-by-string-name-without-performance-overhead/
published: true
post_date: 2014-05-23 15:01:31
---
<p>&#160;</p>  <p>There is no noticeable difference in calling a C# instance method directly or dynamically by &quot;string&quot; name, when you use a cached compiled LINQ expression.</p>  <p>&#160;</p>  <p>In my test case I call a method 1.000.000 times directly and dynamically and both take 1,6s:</p>  <pre class="code">
<span style="background: white; color: blue">namespace </span><span style="background: white; color: black">Research.UnitTests
{
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Microsoft.VisualStudio.TestTools.UnitTesting;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Linq;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Linq.Expressions;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Collections.Generic;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Reflection;

[</span><span style="background: white; color: #2b91af">TestClass</span><span style="background: white; color: black">]
</span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">Research
</span><span style="background: white; color: black">{
[</span><span style="background: white; color: #2b91af">TestMethod</span><span style="background: white; color: black">]
</span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">TestWithTiming()
{
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">watch = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">System.Diagnostics.</span><span style="background: white; color: #2b91af">Stopwatch</span><span style="background: white; color: black">();
    watch.Start();

    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">calculator = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Calculator</span><span style="background: white; color: black">();           

    </span><span style="background: white; color: green">// Get &quot;Calculate&quot; method.
    </span><span style="background: white; color: #2b91af">MethodInfo </span><span style="background: white; color: black">methodInfo = </span><span style="background: white; color: blue">typeof</span><span style="background: white; color: black">(</span><span style="background: white; color: #2b91af">Calculator</span><span style="background: white; color: black">).GetMethod(</span><span style="background: white; color: #a31515">&quot;Calculate&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Type</span><span style="background: white; color: black">[] { </span><span style="background: white; color: blue">typeof</span><span style="background: white; color: black">(</span><span style="background: white; color: blue">int</span><span style="background: white; color: black">) });

    </span><span style="background: white; color: green">// Create parameter &quot;i&quot; for Calculate method.
    </span><span style="background: white; color: #2b91af">ParameterExpression </span><span style="background: white; color: black">param = </span><span style="background: white; color: #2b91af">Expression</span><span style="background: white; color: black">.Parameter(</span><span style="background: white; color: blue">typeof</span><span style="background: white; color: black">(</span><span style="background: white; color: blue">int</span><span style="background: white; color: black">), </span><span style="background: white; color: #a31515">&quot;i&quot;</span><span style="background: white; color: black">);           

    </span><span style="background: white; color: green">// Create &quot;thisParameter&quot; needed to call instance methods.
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">thisParameter = </span><span style="background: white; color: #2b91af">Expression</span><span style="background: white; color: black">.Constant(calculator);

    </span><span style="background: white; color: green">// Create an expression for the method call &quot;Calculate&quot; and specify its parameter(s).
    // If the method was a static method, the &quot;thisParameter&quot; must be removed.
    </span><span style="background: white; color: #2b91af">MethodCallExpression </span><span style="background: white; color: black">methodCall = </span><span style="background: white; color: #2b91af">Expression</span><span style="background: white; color: black">.Call(thisParameter, methodInfo, param);

    </span><span style="background: white; color: green">// Create lambda expression from MethodCallExpression.
    </span><span style="background: white; color: #2b91af">Expression</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">Func</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: blue">int</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt;&gt; lambda = </span><span style="background: white; color: #2b91af">Expression</span><span style="background: white; color: black">.Lambda&lt;</span><span style="background: white; color: #2b91af">Func</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: blue">int</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt;&gt;(
        methodCall,
        </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">ParameterExpression</span><span style="background: white; color: black">[] { param }
    );

    </span><span style="background: white; color: green">// Compile lambda expression to a Func&lt;&gt;.
    </span><span style="background: white; color: #2b91af">Func</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: blue">int</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt; func = lambda.Compile();

    </span><span style="background: white; color: green">// Dynamically call instance method by &quot;name&quot;.
    // Duration: 1620 ms (1,6s).
    </span><span style="background: white; color: blue">for </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">int </span><span style="background: white; color: black">i = 0; i &lt; 1000000; i++)
    {
        </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">result = func(i);
    }

    </span><span style="background: white; color: green">// Direct call
    // Duration: 1605ms (1,6s)
    </span><span style="background: white; color: blue">for </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">int </span><span style="background: white; color: black">i = 0; i &lt; 1000000; i++)
    {
        </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">result = calculator.Calculate(i);
    }

    watch.Stop();
    System.</span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine(watch.Elapsed.TotalMilliseconds);
}
}

</span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">Calculator
</span><span style="background: white; color: black">{
</span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">Calculate(</span><span style="background: white; color: blue">int </span><span style="background: white; color: black">i)
{
    </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">result = </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Empty;

    </span><span style="background: white; color: green">// Execute some code.
    </span><span style="background: white; color: #2b91af">DateTime </span><span style="background: white; color: black">now = </span><span style="background: white; color: #2b91af">DateTime</span><span style="background: white; color: black">.Now;
    </span><span style="background: white; color: #2b91af">DateTime </span><span style="background: white; color: black">nextDay = now.AddDays(i);
    result = nextDay.ToString();

    </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">result;
}
}
}
</span></pre>
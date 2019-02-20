---
ID: 1241
post_title: 'A little command line parser in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/04/16/a-little-command-line-parser-in-c/
published: true
post_date: 2010-04-16 10:48:32
---
<p>If you create a&#160; custom C# console application and want it to use parameters, you must create a command line parser to covert the command line parameters to C# variables.</p>  <p>There are many different ways to pas parameters to a custom C# console application like:</p>  <ul>   <li>MyConsoleApp.exe –Parameter1Name “Parameter1Value” –Parameter2Name “Parameter2Value”</li>    <li>MyConsoleApp.exe “Parameter1Value”,”Parameter2Value”</li>    <li>MyConsoleApp.exe Parameter1Name=”Parameter1Value” Parameter2Name=”Parameter2Value”</li>    <li>etc.</li> </ul>  <p>&#160;</p>  <p>In mine C# console applicaiton I used the format MyConsoleApp.exe Parameter1Name=”Parameter1Value” Parameter2Name=”Parameter2Value”.</p>  <p>To get a specific parameter from the args array, you can use:</p>  <p>&#160;</p>  <p><strong>Usage</strong></p>  <pre class="code"><span style="color: blue">var </span>parser = <span style="color: blue">new </span><span style="color: #2b91af">CommandLineParser</span>();
<span style="color: blue">string </span>parameter1Value = parser.GetValue&lt;<span style="color: blue">string</span>&gt;(<span style="color: #a31515">&quot;Parameter1Name&quot;</span>, args);</pre>

<p>&#160;</p>

<p>&#160;</p>

<p><strong>Class</strong></p>

<p>&#160;</p>

<pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.ComponentModel;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Text;

<span style="color: blue">namespace <font color="#000000">ADAICT</font></span>
{
    <span style="color: blue">public class </span><span style="color: #2b91af">CommandLineParser
    </span>{
        <span style="color: blue">private const string </span>_keyValueSeperator = <span style="color: #a31515">&quot;=&quot;</span>;

        <span style="color: blue">public </span>T GetValue&lt;T&gt;(<span style="color: blue">string </span>key, <span style="color: blue">string</span>[] args)
        {
            <span style="color: blue">if</span>(<span style="color: blue">string</span>.IsNullOrEmpty(key))
            {
                <span style="color: blue">throw new </span><span style="color: #2b91af">NullReferenceException</span>(<span style="color: #a31515">&quot;Parameter [key] can't be null or empty&quot;</span>);
            }
            <span style="color: blue">if </span>(args == <span style="color: blue">null</span>)
            {
                <span style="color: blue">throw new </span><span style="color: #2b91af">NullReferenceException</span>(<span style="color: #a31515">&quot;Parameter [args] can't be null or empty&quot;</span>);
            }

            <span style="color: green">// Select all keyvalue pairs with the given key
            </span><span style="color: blue">var </span>keyValuePairs = <span style="color: blue">from </span>a <span style="color: blue">in </span>args
                      <span style="color: blue">where </span>!<span style="color: blue">string</span>.IsNullOrEmpty(a) &amp;&amp; a.Trim().StartsWith(key + <span style="color: #a31515">&quot;=&quot;</span>)
                      <span style="color: blue">select </span>a.Trim();

            <span style="color: blue">if </span>(keyValuePairs.Count() &gt; 0)
            {
                <span style="color: green">// Get last keyvalue pair with the given key
                </span><span style="color: blue">var </span>lastKeyValuePair = keyValuePairs.Last();
                
                <span style="color: green">// Get the value from the last keyvalue pair with the given key
                </span><span style="color: blue">var </span>value = <span style="color: blue">this</span>.GetValueFromKeyValuePair(lastKeyValuePair);

                <span style="color: green">// Convert the value to the return type
                </span><span style="color: blue">var </span>converter = <span style="color: #2b91af">TypeDescriptor</span>.GetConverter(<span style="color: blue">typeof</span>(T));
                <span style="color: blue">return </span>(T)converter.ConvertFromString(value);
            }
            <span style="color: blue">else
            </span>{
                <span style="color: blue">throw new </span><span style="color: #2b91af">Exception</span>(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;The key [{0}] can't be found on the commandline, make sure it is supplied on the commandline and there are no spaces between the key and the equalsign. Key is case sensitive!&quot;</span>,key));
            }
        }
        <span style="color: blue">public string </span>GetValueFromKeyValuePair(<span style="color: blue">string </span>keyValuePair)
        {
            <span style="color: blue">var </span>result = <span style="color: blue">string</span>.Empty;

            <span style="color: blue">if</span>(!<span style="color: blue">string</span>.IsNullOrEmpty(keyValuePair))
            {
                <span style="color: green">// Split line on &quot;=&quot;
                </span><span style="color: blue">string</span>[] keyValue = keyValuePair.Split(<span style="color: blue">new string</span>[] { _keyValueSeperator }, <span style="color: #2b91af">StringSplitOptions</span>.RemoveEmptyEntries);

                <span style="color: blue">if </span>(keyValue.Length &gt;= 2)
                {
                    <span style="color: green">// Restore the &quot;=&quot; in the value
                    </span>result = <span style="color: #2b91af">String</span>.Join(_keyValueSeperator, keyValue, 1, keyValue.Length - 1);
                }
                <span style="color: blue">else
                </span>{
                    <span style="color: blue">if </span>(keyValue.Length == 1)
                    {
                        <span style="color: green">// value does not contain a &quot;=&quot;
                        </span>result = keyValue[0];
                    }
                }

                <span style="color: green">// Remove leading and trailing quotes
                </span>result = result.Trim(<span style="color: blue">new char</span>[] {<span style="color: #a31515">'&quot;'</span>});
            }

            <span style="color: blue">return </span>result;
        }
    }
}</pre>
<a href="http://11011.net/software/vspaste"></a>
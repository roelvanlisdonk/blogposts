---
ID: 900
post_title: 'Generic C# function for reading a value from registry'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/12/30/generic-c-function-for-reading-a-value-from-registry/
published: true
post_date: 2009-12-30 11:57:47
---
<p>Nice generic read value from registry function on: <a title="http://www.codeproject.com/KB/dotnet/frameworkversiondetection.aspx" href="http://www.codeproject.com/KB/dotnet/frameworkversiondetection.aspx">http://www.codeproject.com/KB/dotnet/frameworkversiondetection.aspx</a>    <br />Function can be called like:    <br /></p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>Microsoft.Win32;
<span style="color: blue">using </span>NUnit.Framework;
<span style="color: blue">using </span>Ada.Cdf.Common;

<span style="color: blue">namespace </span>Ada.Cdf.Test.Common
{
    [<span style="color: #2b91af">TestFixture</span>]
    <span style="color: blue">public class </span><span style="color: #2b91af">RegistryHelperTester
    </span>{
        [<span style="color: #2b91af">Test</span>]
        <span style="color: blue">public void </span>GetRegistryValueTest()
        {
            <span style="color: blue">string </span>data = <span style="color: blue">string</span>.Empty;

            <span style="color: green">// Read a registry key value
            </span><span style="color: blue">bool </span>result = <span style="color: #2b91af">RegistryHelper</span>.GetRegistryValue&lt;<span style="color: blue">string</span>&gt;(<span style="color: #2b91af">RegistryHive</span>.LocalMachine,<span style="color: #a31515">@&quot;SOFTWARE\Microsoft\Windows\CurrentVersion&quot;</span>,<span style="color: #a31515">&quot;ProgramFilesDir&quot;</span>, <span style="color: #2b91af">RegistryValueKind</span>.String, <span style="color: blue">out </span>data);

            <span style="color: green">// Show result
            </span><span style="color: #2b91af">Console</span>.WriteLine(data);
        }
    }
}</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>
  <br /><strong>Result on my machine</strong>

  <br />C:\Program Files (x86)

  <br /></p>

<pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Globalization;
<span style="color: blue">using </span>Microsoft.Win32;

<span style="color: blue">namespace </span>Ada.Cdf.Common
{
    <span style="color: blue">public class </span><span style="color: #2b91af">RegistryHelper
    </span>{
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Read the value of a key from registry
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;typeparam name=&quot;T&quot;&gt;&lt;/typeparam&gt;
        /// &lt;param name=&quot;hive&quot;&gt;&lt;/param&gt;
        /// &lt;param name=&quot;key&quot;&gt;&lt;/param&gt;
        /// &lt;param name=&quot;value&quot;&gt;&lt;/param&gt;
        /// &lt;param name=&quot;kind&quot;&gt;&lt;/param&gt;
        /// &lt;param name=&quot;data&quot;&gt;&lt;/param&gt;
        /// &lt;returns&gt;&lt;/returns&gt;
        </span><span style="color: blue">public static bool </span>GetRegistryValue&lt;T&gt;(<span style="color: #2b91af">RegistryHive </span>hive, <span style="color: blue">string </span>key, <span style="color: blue">string </span>value, <span style="color: #2b91af">RegistryValueKind </span>kind, <span style="color: blue">out </span>T data)
        {
            <span style="color: blue">bool </span>success = <span style="color: blue">false</span>;
            data = <span style="color: blue">default</span>(T);

            <span style="color: blue">using </span>(<span style="color: #2b91af">RegistryKey </span>baseKey = <span style="color: #2b91af">RegistryKey</span>.OpenRemoteBaseKey(hive, <span style="color: #2b91af">String</span>.Empty))
            {
                <span style="color: blue">if </span>(baseKey != <span style="color: blue">null</span>)
                {
                    <span style="color: blue">using </span>(<span style="color: #2b91af">RegistryKey </span>registryKey = baseKey.OpenSubKey(key, <span style="color: #2b91af">RegistryKeyPermissionCheck</span>.ReadSubTree))
                    {
                        <span style="color: blue">if </span>(registryKey != <span style="color: blue">null</span>)
                        {
                            <span style="color: green">// If the key was opened, try to retrieve the value.
                            </span><span style="color: #2b91af">RegistryValueKind </span>kindFound = registryKey.GetValueKind(value);
                            <span style="color: blue">if </span>(kindFound == kind)
                            {
                                <span style="color: blue">object </span>regValue = registryKey.GetValue(value, <span style="color: blue">null</span>);
                                <span style="color: blue">if </span>(regValue != <span style="color: blue">null</span>)
                                {
                                    data = (T)<span style="color: #2b91af">Convert</span>.ChangeType(regValue, <span style="color: blue">typeof</span>(T), <span style="color: #2b91af">CultureInfo</span>.InvariantCulture);
                                    success = <span style="color: blue">true</span>;
                                }
                            }
                        }
                    }
                }
            }
            <span style="color: blue">return </span>success;
        }
    }
}</pre>
<a href="http://11011.net/software/vspaste"></a>
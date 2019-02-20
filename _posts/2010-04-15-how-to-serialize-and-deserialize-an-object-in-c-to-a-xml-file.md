---
ID: 1237
post_title: 'How to serialize and deserialize an object in C# to a XML file'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/04/15/how-to-serialize-and-deserialize-an-object-in-c-to-a-xml-file/
published: true
post_date: 2010-04-15 10:23:47
---
<p>The following code shows how to serialize and deserialize an object in C# to a XML file.</p>  <p>&#160;</p>  <p><strong>Code</strong></p> <a href="http://11011.net/software/vspaste"></a><a href="http://11011.net/software/vspaste"></a>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Text;
<span style="color: blue">using </span>System.IO;
<span style="color: blue">using </span>System.Xml.Serialization;
<span style="color: blue">using </span>System.Reflection;

<span style="color: blue">namespace </span>MobileUI.BC
{
    <span style="color: blue">public class </span><span style="color: #2b91af">SerializationHelper</span>&lt;T&gt; <span style="color: blue">where </span>T : <span style="color: blue">class</span>, <span style="color: blue">new</span>()
    {
        <span style="color: blue">private string </span>_fileName;
        <span style="color: blue">public string </span>FileName
        {
            <span style="color: blue">get
            </span>{
                <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(_fileName))
                {
                    _fileName = <span style="color: #a31515">&quot;Data.xml&quot;</span>;
                }
                <span style="color: blue">return </span>_fileName;
            }
            <span style="color: blue">set
            </span>{
                _fileName = <span style="color: blue">value</span>;
            }
        }
        <span style="color: blue">private </span>T _data;
        <span style="color: blue">public </span>T Data
        {
            <span style="color: blue">get
            </span>{
                <span style="color: blue">if </span>(_data == <span style="color: blue">null</span>)
                {
                    _data = <span style="color: blue">new </span>T();
                }
                <span style="color: blue">return </span>_data;
            }
            <span style="color: blue">set
            </span>{
                _data = <span style="color: blue">value</span>;
            }
        }

        <span style="color: blue">public void </span>Save()
        {
            <span style="color: blue">string </span>filePath = <span style="color: #2b91af">Path</span>.Combine(GetExecutionPath(), FileName);
            
            <span style="color: blue">using </span>(<span style="color: #2b91af">TextWriter </span>writer = <span style="color: blue">new </span><span style="color: #2b91af">StreamWriter</span>(filePath))
            {
                <span style="color: #2b91af">XmlSerializer </span>xs = <span style="color: blue">new </span><span style="color: #2b91af">XmlSerializer</span>(<span style="color: blue">typeof</span>(T));
                xs.Serialize(writer, <span style="color: blue">this</span>.Data);
            }

        }
        <span style="color: blue">public </span>T Load()
        {
            <span style="color: blue">string </span>filePath = <span style="color: #2b91af">Path</span>.Combine(GetExecutionPath(), FileName);

            <span style="color: blue">using </span>(<span style="color: #2b91af">TextReader </span>reader = <span style="color: blue">new </span><span style="color: #2b91af">StreamReader</span>(filePath))
            {
                <span style="color: #2b91af">XmlSerializer </span>xs = <span style="color: blue">new </span><span style="color: #2b91af">XmlSerializer</span>(<span style="color: blue">typeof</span>(T));
                <span style="color: blue">this</span>.Data = xs.Deserialize(reader) <span style="color: blue">as </span>T;
            }

            <span style="color: blue">return this</span>.Data;
        }
        <span style="color: blue">public static string </span>GetExecutionPath()
        {
            <span style="color: blue">string </span>codeBase = <span style="color: #2b91af">Assembly</span>.GetExecutingAssembly().GetName().CodeBase;
            <span style="color: blue">return new </span><span style="color: #2b91af">Uri</span>(<span style="color: #2b91af">Path</span>.GetDirectoryName(codeBase)).LocalPath;
        }
    }
}</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p><strong>Example</strong></p>

<pre class="code">&#160;&#160;&#160;&#160;&#160;&#160;&#160; [<span style="color: #2b91af">TestMethod</span>]
        <span style="color: blue">public void </span>SaveTest()
        {
            <span style="color: #2b91af">Data </span>data = <span style="color: blue">new </span><span style="color: #2b91af">Data</span>();
            data.Days = 2;

            <span style="color: #2b91af">SerializationHelper</span>&lt;<span style="color: #2b91af">Data</span>&gt; sh = <span style="color: blue">new </span><span style="color: #2b91af">SerializationHelper</span>&lt;<span style="color: #2b91af">Data</span>&gt;();
            sh.Data = data;
            sh.Save();
            
            data.Days = 3;
            data = sh.Load();

            <span style="color: #2b91af">Console</span>.WriteLine(data.Days);
        }</pre>
<a href="http://11011.net/software/vspaste"></a>

<p><a href="http://11011.net/software/vspaste"></a></p>

<p>&#160;</p>

<p><strong>Result</strong></p>

<p>2
  <br /><a href="http://11011.net/software/vspaste"></a></p>
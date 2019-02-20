---
ID: 2306
post_title: 'How to serialize an object to string and deserialize a string back to an object in C# 4.0'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/12/20/how-to-serialize-an-object-to-string-and-deserialize-a-string-back-to-an-object-in-c-4-0/
published: true
post_date: 2011-12-20 10:25:12
---
<p>If you want to serialize an object to a string or want to deserialize a string back to an object, you can use the following class:</p>  <p>&#160;</p>  <h3><font style="font-weight: bold">The XmlSerializationTask class</font></h3>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.IO;
<span style="color: blue">using </span>System.Text;
<span style="color: blue">using </span>System.Xml.Serialization;

<span style="color: blue">namespace </span>Rvl.NewCode.Test.Task
{
    <span style="color: gray">/// &lt;summary&gt;
    /// </span><span style="color: green">This class is used for serializing a object to string and back.
    </span><span style="color: gray">/// &lt;/summary&gt;
    /// &lt;typeparam name=&quot;T&quot;&gt;&lt;/typeparam&gt;
    </span><span style="color: blue">public class </span><span style="color: #2b91af">XmlSerializationTask</span>&lt;T&gt; <span style="color: blue">where </span>T : <span style="color: blue">class</span>, <span style="color: blue">new</span>()
    {
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Use this property for types that are unkown at compiletime.
        </span><span style="color: gray">/// &lt;/summary&gt;
        </span><span style="color: blue">public </span><span style="color: #2b91af">Type</span>[] ExtraTypes { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Serializes the object to string.
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;source&quot;&gt;</span><span style="color: green">The source.</span><span style="color: gray">&lt;/param&gt;
        /// &lt;returns&gt;&lt;/returns&gt;
        </span><span style="color: blue">public string </span>SerializeObjectToString(T source)
        {
            <span style="color: #2b91af">StringBuilder </span>result = <span style="color: blue">new </span><span style="color: #2b91af">StringBuilder</span>(<span style="color: blue">string</span>.Empty);
            <span style="color: blue">using </span>(<span style="color: #2b91af">StringWriter </span>writer = <span style="color: blue">new </span><span style="color: #2b91af">StringWriter</span>(result))
            {
                <span style="color: #2b91af">XmlSerializer </span>xs = <span style="color: blue">new </span><span style="color: #2b91af">XmlSerializer</span>(<span style="color: blue">typeof</span>(T), ExtraTypes);
                xs.Serialize(writer, source);
            }
            <span style="color: blue">return </span>result.ToString();
        }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Deserializes from string.
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;source&quot;&gt;</span><span style="color: green">The source.</span><span style="color: gray">&lt;/param&gt;
        /// &lt;returns&gt;&lt;/returns&gt;
        </span><span style="color: blue">public </span>T DeserializeFromString(<span style="color: blue">string </span>source)
        {
            T result;
            <span style="color: blue">using </span>(<span style="color: #2b91af">StringReader </span>reader = <span style="color: blue">new </span><span style="color: #2b91af">StringReader</span>(source))
            {
                <span style="color: #2b91af">XmlSerializer </span>xs = <span style="color: blue">new </span><span style="color: #2b91af">XmlSerializer</span>(<span style="color: blue">typeof</span>(T), ExtraTypes);
                result = xs.Deserialize(reader) <span style="color: blue">as </span>T;
            }
            <span style="color: blue">return </span>result;
        }
    }
}</pre>


<p>&#160;</p>

<h3><font style="font-weight: bold">Using the XmlSerializationTask class</font></h3>


<pre class="code"><span style="color: blue">public void </span>TestXmlSerializationTask()
{
    <span style="color: green">// DynamicTask, is just a class I created with 3 properties:
    </span><span style="color: blue">var </span>dynamicTask = <span style="color: blue">new </span><span style="color: #2b91af">DynamicTask 
    </span>{ 
        Id = <span style="color: #2b91af">Guid</span>.NewGuid(), 
        AssemlbyPath= <span style="color: #2b91af">Environment</span>.NewLine, 
        TypeDescription=<span style="color: #a31515">&quot;Test&quot; 
    </span>};
    <span style="color: blue">var </span>serializeTask = <span style="color: blue">new </span><span style="color: #2b91af">XmlSerializationTask</span>&lt;<span style="color: #2b91af">DynamicTask</span>&gt;();
    <span style="color: blue">string </span>serializedObject = serializeTask.SerializeObjectToString(dynamicTask);
    <span style="color: #2b91af">DynamicTask </span>newDynamicTask = serializeTask.DeserializeFromString(serializedObject);
}</pre>


<h3><font style="font-weight: bold">Produced XML</font></h3>

<p align="left">&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-16&quot;?&gt;
  <br />&lt;DynamicTask xmlns:xsi=&quot;<a href="http://www.w3.org/2001/XMLSchema-instance">http://www.w3.org/2001/XMLSchema-instance&quot;</a> xmlns:xsd=&quot;<a href="http://www.w3.org/2001/XMLSchema&quot;">http://www.w3.org/2001/XMLSchema&quot;</a>&gt;

  <br />&#160; &lt;Id&gt;5b1c6ca4-a8a3-46fc-8496-8caa8c37a47f&lt;/Id&gt;

  <br />&#160; &lt;AssemlbyPath&gt;C:\Temp\Test.dll&lt;/AssemlbyPath&gt;

  <br />&#160; &lt;TypeDescription&gt;Test&lt;/TypeDescription&gt;

  <br />&lt;/DynamicTask&gt;</p>
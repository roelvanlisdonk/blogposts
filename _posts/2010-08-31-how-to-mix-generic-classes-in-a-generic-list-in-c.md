---
ID: 1707
post_title: 'How to mix generic classes in a generic list in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/08/31/how-to-mix-generic-classes-in-a-generic-list-in-c/
published: true
post_date: 2010-08-31 16:00:21
---
<p>If you create a class like Setting&lt;T&gt;, you might think you can create a generic list, like:</p>  <p>List&lt;Setting&lt;T&gt;&gt; List = new List&lt;Setting&lt;T&gt;&gt;();</p>  <p>,but this is not possible in .Net 4.0. If you want objects of type Setting&lt;int&gt; mixed with objects of type&#160; Setting&lt;bool&gt; in one List&lt;T&gt; you must define a none generic base class Setting, like:</p>  <pre class="code"><p><span style="color: blue">    public class </span><span style="color: #2b91af">Setting
    </span>{
        <span style="color: blue">private string </span>_name;
        <span style="color: blue">public string </span>Name
        {
            <span style="color: blue">get
            </span>{
                <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(_name)) { <span style="color: blue"></span></p><p><span style="color: blue">                   throw new </span><span style="color: #2b91af">ApplicationException</span>(<span style="color: #a31515">&quot;Property [Name] in class [Setting] is null or empty&quot;</span>); }
                <span style="color: blue">return </span>_name;
            }
            <span style="color: blue">set </span>{ _name = <span style="color: blue">value</span>; }
        }
    }
    [<span style="color: #2b91af">Serializable</span>]
    <span style="color: blue">public class </span><span style="color: #2b91af">Setting</span>&lt;T&gt; : <span style="color: #2b91af">Setting
    </span>{
        <span style="color: blue">private </span>T _value;
        <span style="color: blue">public </span>T Value
        {
            <span style="color: blue">get
            </span>{
                <span style="color: blue">return </span>_value;
            }
            <span style="color: blue">set
            </span>{
                _value = <span style="color: blue">value</span>;
            }
        }
        <span style="color: blue">public </span><span style="color: #2b91af">Type </span>Type
        {
            <span style="color: blue">get
            </span>{
                <span style="color: blue">return typeof</span>(T);
            }
        }

        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Define a default constructor for serialization purposes
        </span><span style="color: gray">/// &lt;/summary&gt;
        </span><span style="color: blue">public </span>Setting()
        {
        }
    }</p></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>Then you can mix generic types in the generic list like:</p>

<pre class="code"><span style="color: #2b91af">List</span>&lt;<span style="color: #2b91af">Setting</span>&gt; list = <span style="color: blue">new </span><span style="color: #2b91af">List</span>&lt;<span style="color: #2b91af">Setting</span>&gt;
{
    <span style="color: blue">new </span><span style="color: #2b91af">Setting</span>&lt;<span style="color: blue">int</span>&gt;{Name = <span style="color: #a31515">&quot;Timeout&quot;</span>, Value = 1000},
    <span style="color: blue">new </span><span style="color: #2b91af">Setting</span>&lt;<span style="color: blue">bool</span>&gt;{Name = <span style="color: #a31515">&quot;ImportEnabled&quot;</span>, Value = <span style="color: blue">true</span>}
};</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>You can get an element of this list by using the method:</p>

<pre class="code"><span style="color: blue">public </span>T GetSetting&lt;T&gt;(<span style="color: #2b91af">string</span><span style="color: #2b91af"> </span>name, <span style="color: #2b91af">List</span>&lt;<span style="color: #2b91af">Setting</span>&gt; list)
{&#160;&#160;&#160;&#160; T result;
    <span style="color: #2b91af">Setting</span>&lt;T&gt; setting = (<span style="color: #2b91af">Setting</span>&lt;T&gt;)<span style="color: #2b91af">Convert</span>.ChangeType(<br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; list.Single(s =&gt; s.Name.Equals(name)), <span style="color: blue">typeof</span>(<span style="color: #2b91af">Setting</span>&lt;T&gt;), <span style="color: blue">null</span>);
    result = setting.Value;

    <span style="color: blue">return </span>result;
}</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>To call the method use:</p>

<p>int timeout = GetSetting&lt;int&gt;(&quot;Timeout&quot;, list);</p>
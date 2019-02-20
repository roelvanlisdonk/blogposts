---
ID: 742
post_title: 'C# &#8211; Property snippet'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/10/09/c-property-snippet/
published: true
post_date: 2009-10-09 07:43:45
---
<p>Some C# code snippets for C# properties:   <br /></p>  <pre class="code"><span style="color: gray">        /// &lt;summary&gt;
        /// </span><span style="color: green">A object property with null check
        </span><span style="color: gray">/// &lt;/summary&gt;
        </span><span style="color: blue">private </span><span style="color: #2b91af">Type </span>_propertyName = <span style="color: blue">null</span>;
        <span style="color: blue">public </span><span style="color: #2b91af">Type </span>PropertyName
        {
            <span style="color: blue">get
            </span>{
                <span style="color: blue">if</span>(_propertyName == <span style="color: blue">null</span>)
                {
                    <span style="color: blue">throw new </span><span style="color: #2b91af">NullReferenceException</span>(<span style="color: #a31515">&quot;The property [MyClass.PropertyName] can't be null&quot;</span>);
                }
                <span style="color: blue">return </span>_propertyName;
            }
            <span style="color: blue">set
            </span>{
                _propertyName = <span style="color: blue">value</span>;
            }
        }

        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">A string property with empty and null check
        </span><span style="color: gray">/// &lt;/summary&gt;
        </span><span style="color: blue">private string </span>_myString = <span style="color: blue">null</span>;
        <span style="color: blue">public string </span>MyString
        {
            <span style="color: blue">get
            </span>{
                <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(_myString))
                {
                    <span style="color: blue">throw new </span><span style="color: #2b91af">NullReferenceException</span>(<span style="color: #a31515">&quot;The property [MyClass.MyString] can't be null&quot;</span>);
                }
                <span style="color: blue">return </span>_myString;
            }
            <span style="color: blue">set
            </span>{
                _myString = <span style="color: blue">value</span>;
            }
        }</pre>
<a href="http://11011.net/software/vspaste"></a>
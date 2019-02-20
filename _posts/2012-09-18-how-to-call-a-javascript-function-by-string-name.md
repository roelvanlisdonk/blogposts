---
ID: 2834
post_title: >
  How to call a JavaScript function by
  string name.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/09/18/how-to-call-a-javascript-function-by-string-name/
published: true
post_date: 2012-09-18 07:35:04
---
<p>An excellent answer to this question can be found at: <a href="http://stackoverflow.com/questions/359788/how-to-execute-a-javascript-function-when-i-have-its-name-as-a-string">http://stackoverflow.com/questions/359788/how-to-execute-a-javascript-function-when-i-have-its-name-as-a-string</a></p>  <p>I knew you could call a JavaScript function by it’s string name, by using window['functionName'], but this does not work for namespace functions.</p>  <p>When you want to call a namespace function by it’s string name you should use the namespace as context, instead of the window object.</p>   <pre class="code"><span style="color: blue">&lt;!</span><span style="color: maroon">DOCTYPE </span><span style="color: red">html</span><span style="color: blue">&gt;
&lt;</span><span style="color: maroon">html</span><span style="color: blue">&gt;
&lt;</span><span style="color: maroon">head</span><span style="color: blue">&gt;
    &lt;</span><span style="color: maroon">title</span><span style="color: blue">&gt;</span>General testpage.<span style="color: blue">&lt;/</span><span style="color: maroon">title</span><span style="color: blue">&gt;
    &lt;</span><span style="color: maroon">script </span><span style="color: red">src</span><span style="color: blue">=&quot;/Scripts/Kendo/jquery.min.js&quot; </span><span style="color: red">type</span><span style="color: blue">=&quot;text/javascript&quot;&gt;&lt;/</span><span style="color: maroon">script</span><span style="color: blue">&gt;
    &lt;</span><span style="color: maroon">script </span><span style="color: red">type</span><span style="color: blue">=&quot;text/javascript&quot;&gt;
        var </span>MyApp = {};
        MyApp.Navigation = {};
        MyApp.Navigation.refreshDataSources = <span style="color: blue">function </span>()
        {
            alert(<span style="color: maroon">&quot;Alert from refreshDataSources.&quot;</span>);
        };

        <span style="color: #006400">// Dynamically calling namespace function by string name:
        </span>MyApp.Navigation[<span style="color: maroon">&quot;refreshDataSources&quot;</span>]();

        <span style="color: #006400">// Dynamically get namespace part and calling a function in this namespace.
        </span>MyApp[<span style="color: maroon">&quot;Navigation&quot;</span>][<span style="color: maroon">&quot;refreshDataSources&quot;</span>]();            
    <span style="color: blue">&lt;/</span><span style="color: maroon">script</span><span style="color: blue">&gt;
&lt;/</span><span style="color: maroon">head</span><span style="color: blue">&gt;
&lt;</span><span style="color: maroon">body</span><span style="color: blue">&gt;
&lt;/</span><span style="color: maroon">body</span><span style="color: blue">&gt;
&lt;/</span><span style="color: maroon">html</span><span style="color: blue">&gt;
</span></pre>
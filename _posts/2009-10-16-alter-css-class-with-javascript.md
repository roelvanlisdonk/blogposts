---
ID: 760
post_title: >
  Alter CSS class with javascript for
  usage in ASP .NET
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/10/16/alter-css-class-with-javascript/
published: true
post_date: 2009-10-16 11:42:10
---
<p>To alter a CSS class with javascript, you can use the following function:</p>  <pre class="code"><span style="color: green">        // Find the first css class based on parameter [className].
        </span><span style="color: blue">function </span>GetStyleClass(className) {

            <span style="color: green">// Loop all loaded css style sheets
            </span><span style="color: blue">for </span>(<span style="color: blue">var </span>s = 0; s &lt; document.styleSheets.length; s++) {

                <span style="color: green">// Check if browser uses [rules]
                </span><span style="color: blue">var </span>rules;
                <span style="color: blue">if </span>(document.styleSheets[s].rules) {
                    rules = document.styleSheets[s].rules;
                }

                <span style="color: green">// Check if browser uses [cssRules]
                </span><span style="color: blue">if </span>(document.styleSheets[s].cssRules) {
                    rules = document.styleSheets[s].cssRules;
                }

                <span style="color: green">// Check if browser supports css rules
                </span><span style="color: blue">if </span>(rules)
                {
                    <span style="color: green">// Loop rules in css stylesheet
                    </span><span style="color: blue">for </span>(<span style="color: blue">var </span>r = 0; r &lt; rules.length; r++) {

                        <span style="color: green">// Stop search and return rule, when classname is found
                        </span><span style="color: blue">if </span>(rules[r].selectorText == <span style="color: #a31515">'.' </span>+ className) {
                            <span style="color: blue">return </span>rules[r];
                        }
                    }
                }
            }

            <span style="color: green">// If css class not found, return null.
            </span><span style="color: blue">return null</span>;
        }</pre>
Usage of the function in ASP .NET:

<pre class="code"><span style="background: #ffee62">&lt;%</span><span style="color: blue">@ </span><span style="color: #a31515">Page </span><span style="color: red">Language</span><span style="color: blue">=&quot;C#&quot; </span><span style="color: red">AutoEventWireup</span><span style="color: blue">=&quot;true&quot; </span><span style="color: red">CodeBehind</span><span style="color: blue">=&quot;Default.aspx.cs&quot; </span><span style="color: red">Inherits</span><span style="color: blue">=&quot;Rvl.HelperTools.Website._Default&quot; </span><span style="background: #ffee62">%&gt;

</span><span style="color: blue">&lt;!</span><span style="color: #a31515">DOCTYPE </span><span style="color: red">html PUBLIC </span><span style="color: blue">&quot;-//W3C//DTD XHTML 1.0 Transitional//EN&quot; &quot;http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd&quot;&gt;

&lt;</span><span style="color: #a31515">html </span><span style="color: red">xmlns</span><span style="color: blue">=&quot;http://www.w3.org/1999/xhtml&quot; &gt;
&lt;</span><span style="color: #a31515">head </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;</span><span style="color: #a31515">title</span><span style="color: blue">&gt;</span>Untitled Page<span style="color: blue">&lt;/</span><span style="color: #a31515">title</span><span style="color: blue">&gt;

        </span><span style="color: green">&lt;!-- Load css styles --&gt;
    </span><span style="color: blue">&lt;</span><span style="color: #a31515">style </span><span style="color: red">type</span><span style="color: blue">=&quot;text/css&quot;&gt;
        </span><span style="color: #a31515">.Main
        </span>{
            <span style="color: red">background-color</span>:<span style="color: blue">Silver</span>;
            <span style="color: red">margin-left</span>: <span style="color: blue">auto</span>; <span style="color: green">/* Center mainTable for &gt;= IE6  */
            </span><span style="color: red">margin-right</span>: <span style="color: blue">auto</span>; <span style="color: green">/* Center mainTable for &gt;= IE6  */
            </span><span style="color: red">width</span>: <span style="color: blue">800px</span>;
        }
    <span style="color: blue">&lt;/</span><span style="color: #a31515">style</span><span style="color: blue">&gt;

    </span><span style="color: green">&lt;!-- Correct css styles based on user screen resolution --&gt;
    </span><span style="color: blue">&lt;</span><span style="color: #a31515">script </span><span style="color: red">language</span><span style="color: blue">=&quot;javascript&quot; </span><span style="color: red">type</span><span style="color: blue">=&quot;text/javascript&quot;&gt;

        </span><span style="color: green">// Find the first css class based on parameter [className].
        </span><span style="color: blue">function </span>GetStyleClass(className) {

            <span style="color: green">// Loop all loaded css style sheets
            </span><span style="color: blue">for </span>(<span style="color: blue">var </span>s = 0; s &lt; document.styleSheets.length; s++) {

                <span style="color: green">// Check if browser uses [rules]
                </span><span style="color: blue">var </span>rules;
                <span style="color: blue">if </span>(document.styleSheets[s].rules) {
                    rules = document.styleSheets[s].rules;
                }

                <span style="color: green">// Check if browser uses [cssRules]
                </span><span style="color: blue">if </span>(document.styleSheets[s].cssRules) {
                    rules = document.styleSheets[s].cssRules;
                }

                <span style="color: green">// Check if browser supports css rules
                </span><span style="color: blue">if </span>(rules) {
                    <span style="color: green">// Loop rules in css stylesheet
                    </span><span style="color: blue">for </span>(<span style="color: blue">var </span>r = 0; r &lt; rules.length; r++) {

                        <span style="color: green">// Stop search and return rule, when classname is found
                        </span><span style="color: blue">if </span>(rules[r].selectorText == <span style="color: #a31515">'.' </span>+ className) {
                            <span style="color: blue">return </span>rules[r];
                        }
                    }
                }
            }

            <span style="color: green">// If css class not found, return null.
            </span><span style="color: blue">return null</span>;
        }

        <span style="color: green">// Get main table css class
        </span><span style="color: blue">var </span>mainClass = GetStyleClass(<span style="color: #a31515">'Main'</span>);

        <span style="color: green">// Change main table background color if class was found
        </span><span style="color: blue">if </span>(mainClass) {
            mainClass.style.backgroundColor = <span style="color: #a31515">'Red'</span>;
        }
    <span style="color: blue">&lt;/</span><span style="color: #a31515">script</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">head</span><span style="color: blue">&gt;
&lt;</span><span style="color: #a31515">body</span><span style="color: blue">&gt;

    &lt;</span><span style="color: #a31515">form </span><span style="color: red">id</span><span style="color: blue">=&quot;form1&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;</span><span style="color: #a31515">div </span><span style="color: red">class</span><span style="color: blue">=&quot;Main&quot;&gt;
        &lt;</span><span style="color: #a31515">p</span><span style="color: blue">&gt;</span>Some text<span style="color: blue">&lt;/</span><span style="color: #a31515">p</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">p</span><span style="color: blue">&gt;</span>Some more text...<span style="color: blue">&lt;/</span><span style="color: #a31515">p</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">div</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">form</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">body</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">html</span><span style="color: blue">&gt;
</span></pre>
<a href="http://11011.net/software/vspaste"></a>
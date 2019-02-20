---
ID: 762
post_title: >
  Change div or table width and height,
  with CSS rules based on user screen
  resolution in ASP .NET by using
  javascript
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/10/16/change-div-or-table-width-and-height-with-css-rules-based-on-user-screen-resolution-in-asp-net-by-using-javascript/
published: true
post_date: 2009-10-16 11:49:31
---
<p>If you want to change the width of your main div or main table element in ASP .NET, you can use margin-left: auto; and margin-right: auto; to dynamically change the width of these elements based on the browser width, but this width will vary when you change you’re browser screen and older browser (IE6) don’t support the min-width css statement. If you want to have an exact width of the main element you can set the width by using css, but then you will have to choose a fixed value for all user screen resolutions. With the use of javascript, you can change the css value dynamically based on the user screen resolution.</p>  <p>If the main table or main div has an exact width, you can base all other layout inside relative to this width, by using margin’s and padding’s.   <br />    <br /></p>  <pre class="code"><span style="background: #ffee62">&lt;%</span><span style="color: blue">@ </span><span style="color: #a31515">Page </span><span style="color: red">Language</span><span style="color: blue">=&quot;C#&quot; </span><span style="color: red">AutoEventWireup</span><span style="color: blue">=&quot;true&quot; </span><span style="color: red">CodeBehind</span><span style="color: blue">=&quot;Default.aspx.cs&quot; </span><span style="color: red">Inherits</span><span style="color: blue">=&quot;Rvl.HelperTools.Website._Default&quot; </span><span style="background: #ffee62">%&gt;

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
        <span style="color: green">// Convert a css px value to int.
        </span><span style="color: blue">function </span>ConvertCssPxToInt(cssPxValueText) {

            <span style="color: green">// Set valid characters for numeric number.
            </span><span style="color: blue">var </span>validChars = <span style="color: #a31515">&quot;0123456789.&quot;</span>;

            <span style="color: green">// If conversion fails return 0.
            </span><span style="color: blue">var </span>convertedValue = 0;

            <span style="color: green">// Loop all characters of
            </span><span style="color: blue">for </span>(i = 0; i &lt; cssPxValueText.length; i++) {

                <span style="color: green">// Stop search for valid numeric characters,  when a none numeric number is found.
                </span><span style="color: blue">if </span>(validChars.indexOf(cssPxValueText.charAt(i)) == -1) {

                    <span style="color: green">// Start conversion if at least one character is valid.
                    </span><span style="color: blue">if </span>(i &gt; 0) {
                        <span style="color: green">// Convert validnumbers to int and return result.
                        </span>convertedValue = parseInt(cssPxValueText.substring(0, i));
                        <span style="color: blue">return </span>convertedValue;
                    }
                }
            }

            <span style="color: blue">return </span>convertedValue;
        }

        <span style="color: green">// Get main table css class
        </span><span style="color: blue">var </span>mainClass = GetStyleClass(<span style="color: #a31515">'Main'</span>);

        <span style="color: green">// Change main table width based on user screen resolution.
        </span><span style="color: blue">if </span>(mainClass) {

            <span style="color: green">// Use default css width, if screen width is less then default css width.
            </span><span style="color: blue">var </span>width = ConvertCssPxToInt(mainClass.style.width);

            <span style="color: green">// Use screen width - 50px if screen width is greather the default css width.
            </span><span style="color: blue">if </span>(screen.width &gt; width) {
                width = screen.width - 45;
            }

            <span style="color: green">// Change the width of the main table
            </span>mainClass.style.width = width + <span style="color: #a31515">'px'</span>;
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
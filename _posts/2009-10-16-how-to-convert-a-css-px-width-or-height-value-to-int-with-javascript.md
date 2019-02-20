---
ID: 757
post_title: >
  How to convert a CSS px width or height
  value to int with javascript
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/10/16/how-to-convert-a-css-px-width-or-height-value-to-int-with-javascript/
published: true
post_date: 2009-10-16 11:09:53
---
<p>If you want to alter an elements CSS width or height, you must first convert this value to an integer, because the CSS value can have units like px, cm etc.   <br />To convert this value to an integer in javascript, use:</p>  <pre class="code"><span style="color: green">        // Convert a css px value to int.
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
        }</pre>
<a href="http://11011.net/software/vspaste"></a><a href="http://11011.net/software/vspaste"></a>
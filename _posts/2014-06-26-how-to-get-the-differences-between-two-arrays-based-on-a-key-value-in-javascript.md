---
ID: 3873
post_title: 'How to get the differences between two arrays, based on a &ldquo;key&rdquo; value in JavaScript.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/06/26/how-to-get-the-differences-between-two-arrays-based-on-a-key-value-in-javascript/
published: true
post_date: 2014-06-26 15:04:44
---
<p>This page shows how you van use the “getDifferences” function in JavaScript to get the differences between 2 arrays, based on the value of a “key” property.</p>  <pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">!doctype </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">charset</span><span style="background: white; color: blue">=&quot;utf-8&quot;&gt;
&lt;</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">General research page containing only vanilla.js.</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">style </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot;&gt;
    </span><span style="background: white; color: #006400">/* Resets */
    </span><span style="background: white; color: maroon">*</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">*:after</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">*:before </span><span style="background: white; color: black">{
        </span><span style="background: white; color: red">margin</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">; </span><span style="background: white; color: #006400">/* Margin zero is used to prevent unnecessary white space. */
        </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">; </span><span style="background: white; color: #006400">/* Padding zero is used to prevent unnecessary white space. */
        </span><span style="background: white; color: red">-moz-box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">;
        </span><span style="background: white; color: red">-webkit-box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">;
        </span><span style="background: white; color: #006400">/* Border boxing is used, so the padding, margin and borders are within the width and height of de element. */
        </span><span style="background: white; color: red">box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">; 
    }

    </span><span style="background: white; color: maroon">html</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">body </span><span style="background: white; color: black">{
        </span><span style="background: white; color: red">height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">100%</span><span style="background: white; color: black">;
        </span><span style="background: white; color: red">max-height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">100%</span><span style="background: white; color: black">;
    }

    </span><span style="background: white; color: maroon">body </span><span style="background: white; color: black">{
        </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">20px</span><span style="background: white; color: black">;
    }
    </span><span style="background: white; color: maroon">button </span><span style="background: white; color: black">{
        </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">2px 4px 2px 4px</span><span style="background: white; color: black">;
        </span><span style="background: white; color: red">cursor</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">pointer</span><span style="background: white; color: black">;
    }
</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">button </span><span style="background: white; color: red">onclick</span><span style="background: white; color: blue">=&quot;</span><span style="background: white; color: black">app.onExecuteClick(event);</span><span style="background: white; color: blue">&quot;&gt;</span><span style="background: white; color: black">Execute</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">button</span><span style="background: white; color: blue">&gt;

&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot;&gt;
    var </span><span style="background: white; color: black">app = (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
    {
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">self = {};

        self.onExecuteClick = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(e)
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">array1 = [{ Id: 1, Name: </span><span style="background: white; color: #a31515">'Name1' </span><span style="background: white; color: black">}, { Id: 2, Name: </span><span style="background: white; color: #a31515">'Name2' </span><span style="background: white; color: black">}, { Id: 3, Name: </span><span style="background: white; color: #a31515">'Name3' </span><span style="background: white; color: black">}, { Id: 4, Name: </span><span style="background: white; color: #a31515">'Name4' </span><span style="background: white; color: black">}];
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">array2 = [{ Id: 1, Name: </span><span style="background: white; color: #a31515">'Name1' </span><span style="background: white; color: black">}, { Id: 2, Name: </span><span style="background: white; color: #a31515">'Name2' </span><span style="background: white; color: black">}, { Id: 3, Name: </span><span style="background: white; color: #a31515">'Name3' </span><span style="background: white; color: black">}];

            </span><span style="background: white; color: blue">debugger</span><span style="background: white; color: black">;
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">differences = self.getDifferences(array1, array2, </span><span style="background: white; color: #a31515">&quot;Id&quot;</span><span style="background: white; color: black">);
            differences = self.getDifferences(array2, array1, </span><span style="background: white; color: #a31515">&quot;Id&quot;</span><span style="background: white; color: black">);

        };

        self.getDifferences = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(array1, array2, key)
        {
            </span><span style="background: white; color: green">// Directly return arrays, when one array contains elements and the other is empty.
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">array1HasValues = (array1 &amp;&amp; array1.length &amp;&amp; array1.length &gt; 0);
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">array2HasValues = (array2 &amp;&amp; array2.length &amp;&amp; array2.length &gt; 0);
            </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(array1HasValues &amp;&amp; !array2HasValues) { </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">array1; }
            </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(!array1HasValues &amp;&amp; array2HasValues) { </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">array2; }

            </span><span style="background: white; color: green">// Determine biggest and smallest array.
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">biggestArray = (array1.length &gt;= array2.length) ? array1 : array2;
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">smallestArray = (array1.length &gt;= array2.length) ? array2 : array1;               

            </span><span style="background: white; color: green">// Make hashtable of properties &quot;key&quot; in smallestArray
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">smallestKeys = {};
            smallestArray.forEach(</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(obj)
            {
                smallestKeys[obj[key]] = obj;
            });

            </span><span style="background: white; color: green">// Return all elements in biggestArray, unless in smallestArray.
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">differences = biggestArray.filter(</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(obj)
            {
                </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">!(obj[key] </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">smallestKeys);
            });

            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">differences;
        };

        </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">self;
    })();
</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;</span></pre>


<p>&#160;</p>

<p><strong>Result</strong></p>

<p>Result will be the object: <span style="background: white; color: black">{ Id: 4, Name: </span><span style="background: white; color: #a31515">'Name4' </span><span style="background: white; color: black">}</span></p>
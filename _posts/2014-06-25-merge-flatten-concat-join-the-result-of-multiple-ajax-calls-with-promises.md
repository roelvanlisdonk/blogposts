---
ID: 3862
post_title: >
  Merge / Flatten / Concat / Join the
  result of multiple ajax calls with
  promises.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/06/25/merge-flatten-concat-join-the-result-of-multiple-ajax-calls-with-promises/
published: true
post_date: 2014-06-25 15:16:56
---
<p>&#160;</p>  <p>The following code will add a function to the jQuery ($).</p>  <p>It can be used to merge the result of multiple ajax calls.</p>  <p>&#160;</p>  <pre class="code"><span style="background: white; color: black">$.whenall = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">($promises)
{
    </span><span style="background: white; color: green">/// &lt;summary&gt;
    /// Executes the given promises and merges the result to one array.
    /// &lt;/summary&gt;
    /// &lt;param name=&quot;promises&quot; type=&quot;array&quot;&gt;Array of jQuery promises.&lt;/param&gt;
    /// &lt;returns&gt;A promise.&lt;/returns&gt;
    // promises: is aan array of promises.
    </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">$.when.apply($, promises).then(</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
    {
        </span><span style="background: white; color: green">// Convert the special &quot;arguments&quot; object to a real &quot;Array&quot;.
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">args = Array.prototype.slice.call(arguments);

        </span><span style="background: white; color: green">// When the promisses array contains just one element, [args] will be an array containing 3 records: [&quot;array of items&quot;, &quot;promises status&quot;, &quot;promise&quot;].
        // When the promisses array contains more then one element, [args] will be an array of arrays, where each array 3 records: [&quot;array of items&quot;, &quot;promises status&quot;, &quot;promise&quot;].
        // This is handled by only handeling args items that are of type &quot;Array&quot; and foreach handled &quot;Array&quot;, we check if the first item is of type &quot;Array&quot;.
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">merged = [];
        </span><span style="background: white; color: blue">for </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">i = 0, len = args.length; i &lt; len; i++)
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">record = args[i];

            </span><span style="background: white; color: green">// Only handle args items, that are of type &quot;Array&quot;.
            </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(record &amp;&amp; Array.isArray(record) &amp;&amp; record.length &gt; 0)
            {
                </span><span style="background: white; color: green">// Check if first item is of type &quot;Array&quot;.
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">firstItem = record[0];
                </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(Array.isArray(firstItem))
                {
                    merged = merged.concat(firstItem);
                } </span><span style="background: white; color: blue">else
                </span><span style="background: white; color: black">{
                    merged = merged.concat(record);
                }
            }
        }

        </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">merged;
    });
};</span></pre>


<p>&#160;</p>


<p><strong>Example HTML page:</strong></p>


<p>
  <pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">!doctype </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
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
    </span><span style="background: white; color: red">box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">; </span><span style="background: white; color: #006400">/* Border boxing is used, so the padding, margin and borders are within de width and height of de element. */
</span><span style="background: white; color: black">}

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
&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;/Client/Libraries/jQuery/jquery-1.9.1.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;/Client/Libraries/Live/head.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;/Client/Libraries/Live/live.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">button </span><span style="background: white; color: red">onclick</span><span style="background: white; color: blue">=&quot;</span><span style="background: white; color: black">app.onExecuteClick(event);</span><span style="background: white; color: blue">&quot;&gt;</span><span style="background: white; color: black">Execute</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">button</span><span style="background: white; color: blue">&gt;

&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot;&gt;

</span><span style="background: white; color: black">$.whenall = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(promises)
{
    </span><span style="background: white; color: green">// promises: is aan array of promises.
    </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">$.when.apply($, promises).then(</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
    {
        </span><span style="background: white; color: green">// Convert the special &quot;arguments&quot; object to a real &quot;Array&quot;.
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">args = Array.prototype.slice.call(arguments);

        </span><span style="background: white; color: green">// When the promisses array contains just one element, [args] will be an array containing 3 records: [&quot;array of items&quot;, &quot;promises status&quot;, &quot;promise&quot;].
        // When the promisses array contains more then one element, [args] will be an array of arrays, where each array 3 records: [&quot;array of items&quot;, &quot;promises status&quot;, &quot;promise&quot;].
        // This is handled by only handeling args items that are of type &quot;Array&quot; and foreach handled &quot;Array&quot;, we check if the first item is of type &quot;Array&quot;.
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">merged = [];
        </span><span style="background: white; color: blue">for </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">i = 0, len = args.length; i &lt; len; i++)
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">record = args[i];

            </span><span style="background: white; color: green">// Only handle args items, that are of type &quot;Array&quot;.
            </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(record &amp;&amp; Array.isArray(record) &amp;&amp; record.length &gt; 0)
            {
                </span><span style="background: white; color: green">// Check if first item is of type &quot;Array&quot;.
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">firstItem = record[0];
                </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(Array.isArray(firstItem))
                {
                    merged = merged.concat(firstItem);
                } </span><span style="background: white; color: blue">else
                </span><span style="background: white; color: black">{
                    merged = merged.concat(record);
                }
            }
        }

        </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">merged;
    });
};


</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">app = (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
{
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">self = {};
                
    self.handleRestSponse = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(data)
    {
        console.log(data);
    };

    self.onExecuteClick = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(e)
    {
        console.log(</span><span style="background: white; color: #a31515">'onExecuteClick start.'</span><span style="background: white; color: black">);

        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">promises = [];
        promises.push(
            $.ajax({
                url: </span><span style="background: white; color: #a31515">'https://api.github.com/users/roelvanlisdonk/repos'</span><span style="background: white; color: black">,
                type: </span><span style="background: white; color: #a31515">'GET'
            </span><span style="background: white; color: black">})
        );
        promises.push(
            $.ajax({
                url: </span><span style="background: white; color: #a31515">'https://api.github.com/users/roelvanlisdonk/repos'</span><span style="background: white; color: black">,
                type: </span><span style="background: white; color: #a31515">'GET'
            </span><span style="background: white; color: black">})
        );

        $.whenall(promises).then(self.handleRestSponse);

        console.log(</span><span style="background: white; color: #a31515">'onExecuteClick end.'</span><span style="background: white; color: black">);
    };

    </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">self;
})();
</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;</span></pre>
</p>



<p><strong>Result</strong></p>

<p>The arguments is an “array” of 2 objects, each object containing “data”, “promise status”, “promise”.</p>

<p>The merged result is an real array containing the merged “data” objects:</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/06/image13.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/06/image_thumb13.png" width="280" height="385" /></a></p>
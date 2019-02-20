---
ID: 3842
post_title: >
  How to do basic two-way html element
  data binding with Kendo UI.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/06/13/how-to-do-basic-two-way-html-element-data-binding-with-kendo-ui/
published: true
post_date: 2014-06-13 09:16:51
---
<p>To see the code in action, see this Plunker: <a title="http://plnkr.co/SpYSwv" href="http://plnkr.co/SpYSwv">http://plnkr.co/SpYSwv</a></p>  <p>&#160;</p>  <p>The following HTML page shows a input box.</p>  <p>When the users start typing in the input box the SPAN element next to it will show the value just entered (onkeypress).</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/06/image8.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/06/image_thumb8.png" width="244" height="40" /></a></p>  <pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">!DOCTYPE </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">Kendo element binding research page.</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;
        </span><span style="background: white; color: maroon">* </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">margin</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;
        }
        </span><span style="background: white; color: maroon">body </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">20px</span><span style="background: white; color: black">;
        }
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;//cdn.kendostatic.com/2014.1.528/styles/kendo.common.min.css&quot; </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;//cdn.kendostatic.com/2014.1.528/styles/kendo.silver.min.css&quot; </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;//code.jquery.com/jquery-1.9.1.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;//cdn.kendostatic.com/2014.1.528/js/kendo.all.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;view&quot;&gt;
        &lt;</span><span style="background: white; color: maroon">input </span><span style="background: white; color: red">data-bind</span><span style="background: white; color: blue">=&quot;value: inputValue, events: { keypress: showValueOnLabel }&quot; /&gt;
        &lt;</span><span style="background: white; color: maroon">span </span><span style="background: white; color: red">data-bind</span><span style="background: white; color: blue">=&quot;text: label&quot;&gt;&lt;/</span><span style="background: white; color: maroon">span</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
        var </span><span style="background: white; color: black">viewModel = kendo.observable({
            inputValue: </span><span style="background: white; color: #a31515">&quot;Enter some text&quot;</span><span style="background: white; color: black">,
            label: </span><span style="background: white; color: #a31515">&quot;&quot;</span><span style="background: white; color: black">,
            showValueOnLabel: </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(e) {
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">pressedKey = String.fromCharCode(e.charCode);
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">currentValue = e.currentTarget.value;
                </span><span style="background: white; color: blue">this</span><span style="background: white; color: black">.set(</span><span style="background: white; color: #a31515">&quot;label&quot;</span><span style="background: white; color: black">, currentValue + pressedKey);
            }
        });

        kendo.bind($(</span><span style="background: white; color: #a31515">&quot;#view&quot;</span><span style="background: white; color: black">), viewModel);
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;</span></pre>
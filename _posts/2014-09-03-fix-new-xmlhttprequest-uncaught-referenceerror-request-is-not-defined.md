---
ID: 4003
post_title: 'Fix: new XMLHttpRequest() Uncaught ReferenceError: request is not defined'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/09/03/fix-new-xmlhttprequest-uncaught-referenceerror-request-is-not-defined/
published: true
post_date: 2014-09-03 13:25:20
---
<p>I was testing some JavaScript ajax code found at: <a title="http://youmightnotneedjquery.com/" href="http://youmightnotneedjquery.com/">http://youmightnotneedjquery.com/</a> and I was getting the error:</p>  <p>&#160;</p>  <p><font size="1">Uncaught ReferenceError: request is not defined from ReferenceError: request is not defined     <br />&#160;&#160; at Object.rli.app.self.makeXmlHttpRequest (</font><a href="http://localhost:50258/Client/Features/Posts/request_is_not_defined.html:27:25)"><font size="1">http://localhost:50258/Client/Features/Posts/request_is_not_defined.html:27:25)</font></a>    <br /><font size="1">&#160;&#160; at Object.rli.app.self.onExecuteClick (</font><a href="http://localhost:50258/Client/Features/Posts/request_is_not_defined.html:55:22)"><font size="1">http://localhost:50258/Client/Features/Posts/request_is_not_defined.html:55:22)</font></a>    <br /><font size="1">&#160;&#160; at HTMLButtonElement.onclick(</font><a href="http://localhost:50258/Client/Features/Posts/request_is_not_defined.html:12:145)"><font size="1">http://localhost:50258/Client/Features/Posts/request_is_not_defined.html:12:145)</font></a><font size="1"> request_is_not_defined.html:63     <br />Uncaught ReferenceError: request is not defined</font> </p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/09/image.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/09/image_thumb.png" width="580" height="74" /></a></p>  <p>&#160;</p>  <p><strong>Cause</strong></p>  <p>This was caused by the line:</p>  <p><span style="background: white; color: black">request = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">XMLHttpRequest();</span></p>  <p>When you use ‘use strict’, variables need to be defined before use.</p>  <p><strong></strong></p>  <p><strong>Solution</strong></p>  <p>So adding var before request fixed the problem:</p>  <pre class="code"><p><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">!DOCTYPE </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">Vanilla JavaScript.</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">charset</span><span style="background: white; color: blue">=&quot;utf-8&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">http-equiv</span><span style="background: white; color: blue">=&quot;X-UA-Compatible&quot; </span><span style="background: white; color: red">content</span><span style="background: white; color: blue">=&quot;IE=edge, chrome=1&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">name</span><span style="background: white; color: blue">=&quot;viewport&quot; </span><span style="background: white; color: red">content</span><span style="background: white; color: blue">=&quot;width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalable=no&quot; /&gt;
&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;spa-page&quot;&gt;
        &lt;</span><span style="background: white; color: maroon">button </span><span style="background: white; color: red">onclick</span><span style="background: white; color: blue">=&quot;</span><span style="background: white; color: black">rli.app.onExecuteClick()</span><span style="background: white; color: blue">&quot;&gt;</span><span style="background: white; color: black">Execute</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">button</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot;&gt;
        </span><span style="background: white; color: green">// Use a namespace to prevent pollution of the global namespace.
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">rli = rli || {};

        </span><span style="background: white; color: green">// Define application root object.
        </span><span style="background: white; color: black">rli.app = (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
        {
            </span><span style="background: white; color: #a31515">'use strict'</span><span style="background: white; color: black">;

            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">self = {};

            self.makeXmlHttpRequest = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
            {</span></p><p><span style="background: white; color: green">               // When &quot;var&quot; is removed from this line, an error is thrown: <br />               // Uncaught ReferenceError: request is not defined.<br />               </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">request = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">XMLHttpRequest(); </span></p><p><span style="background: white; color: black">                </span><span style="background: white; color: black">request.open(</span><span style="background: white; color: #a31515">'GET'</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">'http://www.google.com'</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">true</span><span style="background: white; color: black">);

                request.onload = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
                {
                    </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">this</span><span style="background: white; color: black">.status &gt;= 200 &amp;&amp; </span><span style="background: white; color: blue">this</span><span style="background: white; color: black">.status &lt; 400)
                    {
                        </span><span style="background: white; color: green">// Success!
                        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">data = JSON.parse(</span><span style="background: white; color: blue">this</span><span style="background: white; color: black">.response);
                        console.log(data);
                    } </span><span style="background: white; color: blue">else
                    </span><span style="background: white; color: black">{
                        </span><span style="background: white; color: green">// We reached our target server, but it returned an error.
                        </span><span style="background: white; color: black">console.log(</span><span style="background: white; color: #a31515">&quot;Error status not between 200 and 400.&quot;</span><span style="background: white; color: black">);
                    }
                };

                request.onerror = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(e)
                {
                    </span><span style="background: white; color: green">// There was a connection error of some sort.
                    </span><span style="background: white; color: black">console.log(e);
                };

                request.send();
            };

            self.onExecuteClick = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
            {
                self.makeXmlHttpRequest();
            };

            self.start = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
            {
                </span><span style="background: white; color: green">// Define global exception handler.
                </span><span style="background: white; color: black">window.onerror = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(message, file, line, col, error)
                {
                    console.log(message, </span><span style="background: white; color: #a31515">&quot;from&quot;</span><span style="background: white; color: black">, error.stack);
                };
            };

            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">self;
        })();

        </span><span style="background: white; color: green">// Start the application.
        </span><span style="background: white; color: black">rli.app.start();
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
</span></p></pre>
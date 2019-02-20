---
ID: 3440
post_title: The best way to load external JavaScript
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/09/12/the-best-way-to-load-external-javascript/
published: true
post_date: 2013-09-12 08:58:36
---
<p>I found another post from Nicholas Zakas interesting: </p>  <p>&#160;</p>  <p>The best way to load external JavaScript </p>  <p><a href="http://www.nczonline.net/blog/2009/07/28/the-best-way-to-load-external-javascript/">http://www.nczonline.net/blog/2009/07/28/the-best-way-to-load-external-javascript/</a> </p>  <p>&#160; </p>  <p><strong>default.html</strong></p>  <pre class="code"><span style="background: white; color: blue">&lt;!</span><span style="background: white; color: maroon">DOCTYPE </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">charset</span><span style="background: white; color: blue">=&quot;utf-8&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">Test page</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;



&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;http://your.cdn.com/first.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot;&gt;
    </span><span style="background: white; color: black">loadScript(</span><span style="background: white; color: #a31515">&quot;http://your.cdn.com/second.js&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
        </span><span style="background: white; color: green">//initialization code
    </span><span style="background: white; color: black">});
</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;</span></pre>

<p><strong>first.js</strong></p>

<pre class="code"><span style="background: white; color: blue">function </span><span style="background: white; color: black">loadScript(url, callback) {

    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">script = document.createElement(</span><span style="background: white; color: #a31515">&quot;script&quot;</span><span style="background: white; color: black">)
    script.type = </span><span style="background: white; color: #a31515">&quot;text/javascript&quot;</span><span style="background: white; color: black">;

    </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(script.readyState) {  </span><span style="background: white; color: green">//IE
        </span><span style="background: white; color: black">script.onreadystatechange = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
            </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(script.readyState == </span><span style="background: white; color: #a31515">&quot;loaded&quot; </span><span style="background: white; color: black">||
                    script.readyState == </span><span style="background: white; color: #a31515">&quot;complete&quot;</span><span style="background: white; color: black">) {
                script.onreadystatechange = </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">;
                callback();
            }
        };
    } </span><span style="background: white; color: blue">else </span><span style="background: white; color: black">{  </span><span style="background: white; color: green">//Others
        </span><span style="background: white; color: black">script.onload = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
            callback();
        };
    }

    script.src = url;
    document.getElementsByTagName(</span><span style="background: white; color: #a31515">&quot;head&quot;</span><span style="background: white; color: black">)[0].appendChild(script);
}</span></pre>
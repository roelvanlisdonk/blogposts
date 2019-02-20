---
ID: 3808
post_title: Jasmine 2.0 reporting html page.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/06/04/jasmine-2-0-reporting-html-page/
published: true
post_date: 2014-06-04 22:09:50
---
<p>Just an example HTML page for reporting Jasmine 2.0 tests.</p>  <p>&#160;</p>  <pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">!doctype </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">html </span><span style="background: white; color: red">lang</span><span style="background: white; color: blue">=&quot;en&quot;&gt;
&lt;</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">charset</span><span style="background: white; color: blue">=&quot;UTF-8&quot;&gt;
    &lt;</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">Jasmine 2.0 example page.</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;jasmine.css&quot; </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;jasmine.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;jasmine-html.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;boot.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;

        </span><span style="background: white; color: green">// This is the function we will test.
        </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">addOne(num) {
            </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">typeof </span><span style="background: white; color: black">num == </span><span style="background: white; color: #a31515">&quot;number&quot;</span><span style="background: white; color: black">) {
                </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">num + 1
            }
            </span><span style="background: white; color: blue">else </span><span style="background: white; color: black">{
                </span><span style="background: white; color: blue">return </span><span style="background: white; color: #a31515">&quot;not a number&quot;
            </span><span style="background: white; color: black">}
        }

        </span><span style="background: white; color: green">// These are the tests.
        </span><span style="background: white; color: black">describe(</span><span style="background: white; color: #a31515">&quot;addOne&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
            it(</span><span style="background: white; color: #a31515">&quot;should be a function&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
                expect(</span><span style="background: white; color: blue">typeof </span><span style="background: white; color: black">addOne).toEqual(</span><span style="background: white; color: #a31515">'function'</span><span style="background: white; color: black">);
            });

            it(</span><span style="background: white; color: #a31515">&quot;should be add one to an integer argument&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
                expect(addOne(1)).toEqual(2);
            });

            describe(</span><span style="background: white; color: #a31515">&quot;when argument is not a number&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
                it(</span><span style="background: white; color: #a31515">&quot;should return 'not a number' when argument is String&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
                    expect(addOne(</span><span style="background: white; color: #a31515">&quot;this is a string&quot;</span><span style="background: white; color: black">)).toEqual(</span><span style="background: white; color: #a31515">&quot;not a number&quot;</span><span style="background: white; color: black">);
                });
            })
        })
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
</span></pre>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/06/image1.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/06/image_thumb1.png" width="543" height="294" /></a></p>
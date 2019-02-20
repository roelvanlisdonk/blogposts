---
ID: 3207
post_title: 'jQuery tip: Add an element as hidden and show on click.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/04/26/jquery-tip-add-an-element-as-hidden-and-show-on-button-click/
published: true
post_date: 2013-04-26 16:54:18
---
<p>If you want to add an element initially as hidden, just <strong>use CSS display: none</strong>.</p>  <p>In the onclick event, use jQuery to show the element.</p>  <p>&#160;</p>  <p>TIP: <strong>Don’t use CSS visibility: hidden</strong>, because this will not work.</p>  <p>&#160;</p>  <pre class="code"><span style="background: white; color: blue">&lt;!</span><span style="background: white; color: maroon">DOCTYPE </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">charset</span><span style="background: white; color: blue">=&quot;utf-8&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">Research</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">style </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot;&gt;
        </span><span style="background: white; color: maroon">#page 
        </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">position</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">relative</span><span style="background: white; color: black">;
        }
        </span><span style="background: white; color: maroon">span.action 
        </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">cursor</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">pointer</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">text-decoration</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">underline</span><span style="background: white; color: black">;
        }
        </span><span style="background: white; color: maroon">#elementToShow 
        </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">position</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">absolute</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">width</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">100px</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">left</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">30px</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">top</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">60px</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">display</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">none</span><span style="background: white; color: black">;
            </span><span style="background: white; color: #006400">/* visibility: hidden; */ /* &lt;== This will not work*/
        </span><span style="background: white; color: black">}
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;Scripts/jquery-2.0.0.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot;&gt;
        </span><span style="background: white; color: black">App = {};
        $(document).ready(</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
        {
            
        });
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;page&quot;&gt;
        &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;elementToShow&quot;&gt;</span><span style="background: white; color: black">Hello world!</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">span </span><span style="background: white; color: red">onclick</span><span style="background: white; color: blue">=&quot;$('#elementToShow').show();&quot; </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;action&quot;&gt;</span><span style="background: white; color: black">show</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">span</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">span </span><span style="background: white; color: red">onclick</span><span style="background: white; color: blue">=&quot;$('#elementToShow').hide();&quot; </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;action&quot;&gt;</span><span style="background: white; color: black">hide</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">span</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;</span></pre>

<p>Initial</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/04/image4.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/04/image_thumb4.png" width="130" height="69" /></a></p>

<p>After clicking on &quot;show&quot;</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/04/image5.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/04/image_thumb5.png" width="226" height="149" /></a></p>
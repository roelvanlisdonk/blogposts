---
ID: 3831
post_title: >
  Create kendo ui tooltip with template
  and correct position on element click.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/06/11/create-kendo-ui-tooltip-with-template-and-correct-position-on-element-click/
published: true
post_date: 2014-06-11 15:26:19
---
<p>Just a code snippet, that shows a tooltip, when the user clicks on a button:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/06/image7.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/06/image_thumb7.png" width="580" height="318" /></a></p>  <p>&#160;</p>  <pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">!DOCTYPE </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">RLI research page.</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot; </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;../../../Libraries/Kendo/styles/kendo.common.min.css&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot; </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;../../../Libraries/Kendo/styles/kendo.rtl.min.css&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot; </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;../../../Libraries/Kendo/styles/kendo.metro.min.css&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot; </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;../../../Libraries/FontAwesome/css/font-awesome.min.css&quot; /&gt;</span><span style="background: white; color: blue">
    &lt;</span><span style="background: white; color: maroon">style </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot;&gt;
        </span><span style="background: white; color: maroon">#toonTooltip_tt_active </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">background-color</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">#FFFFFF</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">left</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">14px</span><span style="background: white; color: black">;
        }
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;page&quot;&gt;
        &lt;</span><span style="background: white; color: maroon">h3 </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;page-header&quot;&gt;</span><span style="background: white; color: black">RLI research page.</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">h3</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;content&quot;&gt;
            &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">style</span><span style="background: white; color: blue">=&quot;</span><span style="background: white; color: red">position</span><span style="background: white; color: black">:</span><span style="background: white; color: blue">absolute</span><span style="background: white; color: black">;</span><span style="background: white; color: red">top</span><span style="background: white; color: black">:</span><span style="background: white; color: blue">100px</span><span style="background: white; color: black">;</span><span style="background: white; color: blue">&quot;&gt;&lt;</span><span style="background: white; color: maroon">button </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;toonTooltip&quot; </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;button&quot;&gt;</span><span style="background: white; color: black">...</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">button</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
        &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;

        &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/x-kendo-template&quot; </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;template&quot;&gt;
            &lt;</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
                &lt;</span><span style="background: white; color: maroon">button </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;button&quot; </span><span style="background: white; color: red">style</span><span style="background: white; color: blue">=&quot;</span><span style="background: white; color: red">margin-top</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">4px</span><span style="background: white; color: black">; </span><span style="background: white; color: red">margin-bottom</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">4px</span><span style="background: white; color: black">; </span><span style="background: white; color: red">width</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">200px</span><span style="background: white; color: black">;</span><span style="background: white; color: blue">&quot;&gt;</span><span style="background: white; color: black">Exporteer to .csv</span><span style="background: white; color: red">&amp;nbsp;</span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">i </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;fa fa-file-text-o&quot; </span><span style="background: white; color: red">title</span><span style="background: white; color: blue">=&quot;Exporteer to *.csv.&quot;&gt;&lt;/</span><span style="background: white; color: maroon">i</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: maroon">button</span><span style="background: white; color: blue">&gt;
            &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
                &lt;</span><span style="background: white; color: maroon">button </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;button&quot; </span><span style="background: white; color: red">style</span><span style="background: white; color: blue">=&quot;</span><span style="background: white; color: red">margin-bottom</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">4px</span><span style="background: white; color: black">; </span><span style="background: white; color: red">width</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">200px</span><span style="background: white; color: black">;</span><span style="background: white; color: blue">&quot;&gt;</span><span style="background: white; color: black">Exporteer naar .kml</span><span style="background: white; color: red">&amp;nbsp;</span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">i </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;fa fa-file-text-o&quot; </span><span style="background: white; color: red">title</span><span style="background: white; color: blue">=&quot;Exporteer to *.kml.&quot;&gt;&lt;/</span><span style="background: white; color: maroon">i</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: maroon">button</span><span style="background: white; color: blue">&gt;
            &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
                &lt;</span><span style="background: white; color: maroon">button </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;button&quot; </span><span style="background: white; color: red">style</span><span style="background: white; color: blue">=&quot;</span><span style="background: white; color: red">margin-bottom</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">4px</span><span style="background: white; color: black">; </span><span style="background: white; color: red">width</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">200px</span><span style="background: white; color: black">;</span><span style="background: white; color: blue">&quot;&gt;</span><span style="background: white; color: black">Show route</span><span style="background: white; color: red">&amp;nbsp;</span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">i </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;fa fa-road&quot; </span><span style="background: white; color: red">title</span><span style="background: white; color: blue">=&quot;Show route.&quot;&gt;&lt;/</span><span style="background: white; color: maroon">i</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: maroon">button</span><span style="background: white; color: blue">&gt;
            &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
                &lt;</span><span style="background: white; color: maroon">button </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;button&quot; </span><span style="background: white; color: red">style</span><span style="background: white; color: blue">=&quot;</span><span style="background: white; color: red">margin-bottom</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">4px</span><span style="background: white; color: black">; </span><span style="background: white; color: red">width</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">200px</span><span style="background: white; color: black">;</span><span style="background: white; color: blue">&quot;&gt;</span><span style="background: white; color: black">Delete route</span><span style="background: white; color: red">&amp;nbsp;</span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">i </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;fa fa-minus-square&quot; </span><span style="background: white; color: red">title</span><span style="background: white; color: blue">=&quot;Delete route.&quot;&gt;&lt;/</span><span style="background: white; color: maroon">i</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: maroon">button</span><span style="background: white; color: blue">&gt;
            &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
        &lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;../../../Libraries/jQuery/jquery-1.10.2.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: blue">
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;../../../Libraries/Kendo/js/kendo.web.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;../../../Libraries/Kendo/js/cultures/kendo.culture.nl-NL.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
</span><span style="background: white; color: #006400">    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;Rli.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
</span></pre>


<p>&#160;</p>

<p><strong>Rli.js</strong></p>

<pre class="code"><span style="background: white; color: blue">var </span><span style="background: white; color: black">app = (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
{
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">self = </span><span style="background: white; color: blue">this</span><span style="background: white; color: black">;
    
    </span><span style="background: white; color: green">// The &quot;main&quot; entry point for this application.
    </span><span style="background: white; color: black">self.start = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
    {
        </span><span style="background: white; color: black">$(</span><span style="background: white; color: #a31515">&quot;#toonTooltip&quot;</span><span style="background: white; color: black">).kendoTooltip({
            autoHide: </span><span style="background: white; color: blue">false</span><span style="background: white; color: black">,
            content: kendo.template($(</span><span style="background: white; color: #a31515">&quot;#template&quot;</span><span style="background: white; color: black">).html()),
            position: </span><span style="background: white; color: #a31515">&quot;right&quot;</span><span style="background: white; color: black">,
            showOn: </span><span style="background: white; color: #a31515">&quot;click&quot;
        </span><span style="background: white; color: black">});
    };

    </span><span style="background: white; color: black">    
    </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">self;
})();

</span><span style="background: white; color: green">// Start the application.
</span><span style="background: white; color: black">app.start();</span></pre>
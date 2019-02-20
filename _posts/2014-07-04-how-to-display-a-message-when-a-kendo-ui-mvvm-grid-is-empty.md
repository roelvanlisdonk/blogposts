---
ID: 3920
post_title: >
  How to display a message, when a Kendo
  UI MVVM grid is empty.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/07/04/how-to-display-a-message-when-a-kendo-ui-mvvm-grid-is-empty/
published: true
post_date: 2014-07-04 15:28:27
---
<p>If you want to show an text in a Kendo UI grid, you could use CSS, as suggested on stackoverflow.com:</p>  <p><a title="http://stackoverflow.com/questions/23476978/display-a-message-within-the-kendo-grid-when-its-empty" href="http://stackoverflow.com/questions/23476978/display-a-message-within-the-kendo-grid-when-its-empty">http://stackoverflow.com/questions/23476978/display-a-message-within-the-kendo-grid-when-its-empty</a></p>  <p>&#160;</p>  <p>But if you want to completely hide the gird and show a message, you can use a calculated field:</p>  <p><a title="http://docs.telerik.com/kendo-ui/getting-started/framework/mvvm/observableobject#creating-dependent-methods-also-known-as-calculated-fields" href="http://docs.telerik.com/kendo-ui/getting-started/framework/mvvm/observableobject#creating-dependent-methods-also-known-as-calculated-fields">http://docs.telerik.com/kendo-ui/getting-started/framework/mvvm/observableobject#creating-dependent-methods-also-known-as-calculated-fields</a></p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image12.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image_thumb12.png" width="580" height="83" /></a></p>  <p>&#160;</p>  <p><strong>HTML</strong></p>  <pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">!DOCTYPE </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">Kendo element binding research page.</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot; </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;//cdn.kendostatic.com/2014.1.528/styles/kendo.common.min.css&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot; </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;//cdn.kendostatic.com/2014.1.528/styles/kendo.rtl.min.css&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot; </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;//cdn.kendostatic.com/2014.1.528/styles/kendo.metro.min.css&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot; </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;//cdn.kendostatic.com/2014.1.528/styles/kendo.metro.mobile.min.css&quot; /&gt;
</span><span style="background: white; color: blue">    &lt;</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;
        </span><span style="background: white; color: #006400">/* Resets */
        </span><span style="background: white; color: maroon">div</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">span</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">i</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">p</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">input</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">select </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">-moz-box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">-webkit-box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">; </span><span style="background: white; color: #006400">/* Border boxing is used, so the padding, margin and borders are within the width and height of de element. */
            </span><span style="background: white; color: red">color</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">rgb(112, 112, 112)</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">font-family</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">Arial</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">Helvetica</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">sans-serif</span><span style="background: white; color: black">; </span><span style="background: white; color: #006400">/* For know use default fonts used on google.com stackoverflow.com, telerik.com etc. */
            </span><span style="background: white; color: red">font-size</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">13px</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">margin</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">; </span><span style="background: white; color: #006400">/* Margin zero is used to prevent unnecessary white space. */
            </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">; </span><span style="background: white; color: #006400">/* Padding zero is used to prevent unnecessary white space. */
        </span><span style="background: white; color: black">}        

        </span><span style="background: white; color: maroon">html</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">body </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">100%</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">max-height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">100%</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: maroon">body </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">20px</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: maroon">.info </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">border</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">1px solid rgb(128, 128, 128)</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">box-shadow</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">rgba(0, 0, 0, 0.298039) 0 2px 6px 0</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">rgba(0, 0, 0, 0.2) 0 -3px 8px 0</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">10px</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: maroon">.no-data </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">border</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">1px solid #dadada</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">10px</span><span style="background: white; color: black">;
        }
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;view&quot;&gt;
        &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;info&quot;&gt;            
            &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;productsRowTemplate&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/x-kendo-tmpl&quot;&gt;
                &lt;</span><span style="background: white; color: maroon">tr </span><span style="background: white; color: red">data-uid</span><span style="background: white; color: blue">=&quot;#: uid#&quot;&gt;
                    &lt;</span><span style="background: white; color: maroon">td</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">#: Id#</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">td</span><span style="background: white; color: blue">&gt;
                    &lt;</span><span style="background: white; color: maroon">td</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">#: Name#</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">td</span><span style="background: white; color: blue">&gt;
                &lt;/</span><span style="background: white; color: maroon">tr</span><span style="background: white; color: blue">&gt;
            &lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;productsGrid&quot; </span><span style="background: white; color: red">data-role</span><span style="background: white; color: blue">=&quot;grid&quot;
                 </span><span style="background: white; color: red">data-row-template</span><span style="background: white; color: blue">=&quot;productsRowTemplate&quot;
                 </span><span style="background: white; color: red">data-columns</span><span style="background: white; color: blue">=&quot;[
                                    { 'field': 'Id' },
                                    { 'field': 'Name' }
                               ]&quot;
                 </span><span style="background: white; color: red">data-bind</span><span style="background: white; color: blue">=&quot;source: products, invisible: productsIsEmpty&quot;&gt;&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;no-data&quot; </span><span style="background: white; color: red">data-bind</span><span style="background: white; color: blue">=&quot;visible: productsIsEmpty&quot;&gt;</span><span style="background: white; color: black">No data.</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
        &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;

    </span><span style="background: white; color: #006400">&lt;!-- Libraries --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;//code.jquery.com/jquery-1.9.1.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;//cdn.kendostatic.com/2014.1.528/js/kendo.all.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
</span><span style="background: white; color: blue">

    </span><span style="background: white; color: #006400">&lt;!-- Custom --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;kendo-controller.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;</span></pre>


<p>&#160;</p>

<p><strong>JavaScript</strong></p>

<pre class="code"><span style="background: white; color: blue">var </span><span style="background: white; color: black">kendo = kendo || {};

kendo.controller = (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">self = {};
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">_vm = </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">;

    self.show = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {

        _vm = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">kendo.data.ObservableObject({
            products: </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">kendo.data.DataSource({
                data: </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">kendo.data.ObservableArray([
                    
                ])
            }),
            productsIsEmpty: </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
                </span><span style="background: white; color: blue">return this</span><span style="background: white; color: black">.get(</span><span style="background: white; color: #a31515">&quot;products&quot;</span><span style="background: white; color: black">).data().length === 0;
            }
        });

        kendo.bind($(</span><span style="background: white; color: #a31515">&quot;#view&quot;</span><span style="background: white; color: black">), _vm);
    };

    </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">self;
})();

kendo.controller.show();</span></pre>
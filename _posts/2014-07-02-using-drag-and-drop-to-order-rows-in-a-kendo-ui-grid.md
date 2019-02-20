---
ID: 3889
post_title: >
  Using drag and drop to order rows in a
  Kendo UI grid
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/07/02/using-drag-and-drop-to-order-rows-in-a-kendo-ui-grid/
published: true
post_date: 2014-07-02 09:53:18
---
<p>&#160;</p>  <p><strong>Before drag and drop</strong></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image1.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image_thumb1.png" width="580" height="141" /></a></p>  <p><strong>During drag and drop</strong></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image2.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image_thumb2.png" width="580" height="134" /></a></p>  <p>&#160;</p>  <p><strong>After drag and drop</strong></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image3.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image_thumb3.png" width="580" height="141" /></a></p>  <p>&#160;</p>  <p><strong>Code</strong></p>  <pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">!DOCTYPE </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">Kendo element binding research page.</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot; </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;//cdn.kendostatic.com/2014.1.528/styles/kendo.common.min.css&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot; </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;//cdn.kendostatic.com/2014.1.528/styles/kendo.rtl.min.css&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot; </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;//cdn.kendostatic.com/2014.1.528/styles/kendo.metro.min.css&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot; </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;//cdn.kendostatic.com/2014.1.528/styles/kendo.metro.mobile.min.css&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot; </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;//netdna.bootstrapcdn.com/font-awesome/4.1.0/css/font-awesome.min.css&quot;&gt;
    &lt;</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;
        </span><span style="background: white; color: #006400">/* Resets */
        </span><span style="background: white; color: maroon">* </span><span style="background: white; color: black">{
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

        </span><span style="background: white; color: maroon">.addressRow </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">cursor</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">move</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">cursor</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">-webkit-grab</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">cursor</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">-moz-grab</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">10px</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">line-height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">10px</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">margin</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;
        }

            </span><span style="background: white; color: maroon">.addressRow input </span><span style="background: white; color: black">{
                </span><span style="background: white; color: red">font-family</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">FontAwesome</span><span style="background: white; color: black">;
            }

        </span><span style="background: white; color: maroon">#addressGrid tr &gt; td </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">1.6em</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">line-height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">1.6em</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">1px 4px 1px 4px</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">margin</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: maroon">#addressGrid tr &gt; th </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">font-weight</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">bold</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">1.6em</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">line-height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">1.6em</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">margin</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">1px 4px 1px 4px</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: maroon">#addressGrid tr &gt; td:first-child</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">#addressGrid tr &gt; th:first-child </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">width</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">56px</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: maroon">#addressGrid tr:last-child td </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">padding-bottom</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">3px</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: maroon">.km-switch </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">cursor</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">pointer</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">1.6em</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">line-height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">1.6em</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">margin</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: maroon">#addressGrid tr &gt; td:first-child .km-switch-label-on</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">#addressGrid tr &gt; td:first-child .km-switch-label-off </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">font-family</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">FontAwesome</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">color</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">rgb(112, 112, 112)</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">1.6em</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">line-height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">1.6em</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: maroon">#addressGrid tr &gt; td:first-child .km-switch-label-on:before </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">content</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">&quot;\f023&quot;</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: maroon">#addressGrid tr &gt; td:first-child .km-switch-label-off:before </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">content</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">&quot;\f09c&quot;</span><span style="background: white; color: black">;
        }
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;

&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;view&quot;&gt;
        &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;info&quot;&gt;
            &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;addressRowTemplate&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/x-kendo-tmpl&quot;&gt;
                &lt;</span><span style="background: white; color: maroon">tr </span><span style="background: white; color: red">data-uid</span><span style="background: white; color: blue">=&quot;#: uid#&quot; </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;addressRow&quot;&gt;
                    &lt;</span><span style="background: white; color: maroon">td</span><span style="background: white; color: blue">&gt;
                        &lt;</span><span style="background: white; color: maroon">input </span><span style="background: white; color: red">data-role</span><span style="background: white; color: blue">=&quot;switch&quot; </span><span style="background: white; color: red">data-on-label</span><span style="background: white; color: blue">=&quot;&quot; </span><span style="background: white; color: red">data-off-label</span><span style="background: white; color: blue">=&quot;&quot; </span><span style="background: white; color: red">data-bind</span><span style="background: white; color: blue">=&quot;checked: IsFixed&quot;&gt;
                    &lt;/</span><span style="background: white; color: maroon">td</span><span style="background: white; color: blue">&gt;
                    &lt;</span><span style="background: white; color: maroon">td</span><span style="background: white; color: blue">&gt;
                        </span><span style="background: white; color: black">#: Address#
                    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">td</span><span style="background: white; color: blue">&gt;
                    &lt;</span><span style="background: white; color: maroon">td</span><span style="background: white; color: blue">&gt;
                        </span><span style="background: white; color: black">#: Lat#
                    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">td</span><span style="background: white; color: blue">&gt;
                    &lt;</span><span style="background: white; color: maroon">td</span><span style="background: white; color: blue">&gt;
                        </span><span style="background: white; color: black">#: Long#
                    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">td</span><span style="background: white; color: blue">&gt;
                    &lt;</span><span style="background: white; color: maroon">td</span><span style="background: white; color: blue">&gt;
                        &lt;</span><span style="background: white; color: maroon">input </span><span style="background: white; color: red">data-role</span><span style="background: white; color: blue">=&quot;switch&quot; </span><span style="background: white; color: red">data-on-label</span><span style="background: white; color: blue">=&quot;Y&quot; </span><span style="background: white; color: red">data-off-label</span><span style="background: white; color: blue">=&quot;N&quot; </span><span style="background: white; color: red">data-bind</span><span style="background: white; color: blue">=&quot;checked: IsFixed&quot;&gt;
                    &lt;/</span><span style="background: white; color: maroon">td</span><span style="background: white; color: blue">&gt;
                &lt;/</span><span style="background: white; color: maroon">tr</span><span style="background: white; color: blue">&gt;
            &lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;addressGrid&quot; </span><span style="background: white; color: red">data-role</span><span style="background: white; color: blue">=&quot;grid&quot;
                 </span><span style="background: white; color: red">data-row-template</span><span style="background: white; color: blue">=&quot;addressRowTemplate&quot;
                 </span><span style="background: white; color: red">data-columns</span><span style="background: white; color: blue">=&quot;[
                                    { 'field': 'IsFixed' },
                                    { 'field': 'Address' },
                                    { 'field': 'Lat' },
                                    { 'field': 'Long' },
                                    { 'field': 'Selected' }
                               ]&quot;
                 </span><span style="background: white; color: red">data-bind</span><span style="background: white; color: blue">=&quot;source: addresses&quot;&gt;&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
        &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;//code.jquery.com/jquery-1.9.1.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;//cdn.kendostatic.com/2014.1.528/js/kendo.all.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;/Client/Libraries/Live/head.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;/Client/Libraries/Live/live.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot;&gt;
        </span><span style="background: white; color: black">kendo.addDragAndDropToGrid = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(gridId, rowClass, viewModel, validateDropTargetFunc)
        {
            </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(!gridId) { </span><span style="background: white; color: blue">throw </span><span style="background: white; color: #a31515">&quot;Parameter [gridId] is not set.&quot;</span><span style="background: white; color: black">; }
            </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(!rowClass) { </span><span style="background: white; color: blue">throw </span><span style="background: white; color: #a31515">&quot;Parameter [rowClass] is not set.&quot;</span><span style="background: white; color: black">; }

            $(rowClass).kendoDraggable({
                hint: </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(element)
                {
                    </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">element.clone();
                }
            });

            $(gridId).kendoDropTargetArea({
                filter: rowClass,
                drop: </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(e)
                {
                    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">srcUid = e.draggable.element.data(</span><span style="background: white; color: #a31515">&quot;uid&quot;</span><span style="background: white; color: black">);
                    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">dstUid = e.dropTarget.data(</span><span style="background: white; color: #a31515">&quot;uid&quot;</span><span style="background: white; color: black">);
                    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">ds = $(gridId).data(</span><span style="background: white; color: #a31515">&quot;kendoGrid&quot;</span><span style="background: white; color: black">).dataSource;
                    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">srcItem = ds.getByUid(srcUid);
                    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">dstItem = ds.getByUid(dstUid);
                    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">dstIdx = ds.indexOf(dstItem);
                    ds.remove(srcItem);
                    ds.insert(dstIdx, srcItem);
                    e.draggable.destroy();
                    kendo.addDragAndDropToGrid(gridId, rowClass, viewModel, validateDropTargetFunc);
                }
            });
        };

        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">dataService = (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
        {
            </span><span style="background: white; color: #a31515">&quot;use strict&quot;</span><span style="background: white; color: black">;
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">self = {};

            self.getAddresses = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
            {
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">data = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">kendo.data.ObservableArray(
                [
                    { Id: 1, Address: </span><span style="background: white; color: #a31515">'Kerkweg 22'</span><span style="background: white; color: black">,   Lat: </span><span style="background: white; color: #a31515">'52.367443'</span><span style="background: white; color: black">, Long: </span><span style="background: white; color: #a31515">'4.865275'</span><span style="background: white; color: black">, Selected: </span><span style="background: white; color: blue">false</span><span style="background: white; color: black">, IsFixed: </span><span style="background: white; color: blue">false </span><span style="background: white; color: black">},
                    { Id: 2, Address: </span><span style="background: white; color: #a31515">'Peilstraat 3'</span><span style="background: white; color: black">, Lat: </span><span style="background: white; color: #a31515">'52.367967'</span><span style="background: white; color: black">, Long: </span><span style="background: white; color: #a31515">'4.866217'</span><span style="background: white; color: black">, Selected: </span><span style="background: white; color: blue">false</span><span style="background: white; color: black">, IsFixed: </span><span style="background: white; color: blue">true </span><span style="background: white; color: black">},
                    { Id: 3, Address: </span><span style="background: white; color: #a31515">'Bakkerloop 35'</span><span style="background: white; color: black">, Lat: </span><span style="background: white; color: #a31515">'52.367946'</span><span style="background: white; color: black">, Long: </span><span style="background: white; color: #a31515">'4.865482'</span><span style="background: white; color: black">, Selected: </span><span style="background: white; color: blue">false</span><span style="background: white; color: black">, IsFixed: </span><span style="background: white; color: blue">false </span><span style="background: white; color: black">},
                    { Id: 4, Address: </span><span style="background: white; color: #a31515">'Eikenlaan 1'</span><span style="background: white; color: black">, Lat: </span><span style="background: white; color: #a31515">'52.368237'</span><span style="background: white; color: black">, Long: </span><span style="background: white; color: #a31515">'4.866694'</span><span style="background: white; color: black">, Selected: </span><span style="background: white; color: blue">false</span><span style="background: white; color: black">, IsFixed: </span><span style="background: white; color: blue">true </span><span style="background: white; color: black">}
                ]);

                </span><span style="background: white; color: green">// Manual create a promise, so this function mimicks an Ajax call.
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">dfd = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">$.Deferred();
                dfd.resolve(data);

                </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">dfd.promise();
            };

            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">self;
        })(kendo);

        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">viewModel = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">kendo.observable({
            addresses: </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">kendo.data.DataSource({ data: [] })
        });

        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">controller = (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(dataService, viewModel)
        {
            </span><span style="background: white; color: #a31515">&quot;use strict&quot;</span><span style="background: white; color: black">;
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">_dataService = dataService;            
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">_vm = viewModel;
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">self = {};
                        
            self.handleAdressesRefresh = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(data)
            {
                _vm.set(</span><span style="background: white; color: #a31515">&quot;addresses&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">kendo.data.DataSource({ data: data }));
                kendo.bind($(</span><span style="background: white; color: #a31515">&quot;.info&quot;</span><span style="background: white; color: black">), _vm);
                kendo.addDragAndDropToGrid(</span><span style="background: white; color: #a31515">&quot;#addressGrid&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;.addressRow&quot;</span><span style="background: white; color: black">, _vm);
            };

            self.show = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
            {
                $.when(_dataService.getAddresses())
                .then(self.handleAdressesRefresh);
            };

            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">self;
        })(dataService, viewModel);

        controller.show();
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;</span></pre>
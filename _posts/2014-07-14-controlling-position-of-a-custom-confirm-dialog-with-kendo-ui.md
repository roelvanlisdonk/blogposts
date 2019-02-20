---
ID: 3957
post_title: >
  Controlling position of a custom confirm
  dialog with Kendo UI
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/07/14/controlling-position-of-a-custom-confirm-dialog-with-kendo-ui/
published: true
post_date: 2014-07-14 09:41:02
---
<p>The native confirm dialog, shown when you use the confirm function in JavaScript can’t be positioned in JavaScript.</p>  <p>A Kendo UI window can be positioned.</p>  <p>&#160;</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image21.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image_thumb21.png" width="580" height="354" /></a></p>  <p>&#160;</p>  <p><strong>HTML</strong></p>  <pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">!DOCTYPE </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
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
        </span><span style="background: white; color: maroon">div</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">span</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">i</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">p</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">input</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">select </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">-moz-box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">-webkit-box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">; </span><span style="background: white; color: #006400">/* Border boxing is used, so the padding, margin and borders are within the width and height of de element. */
            </span><span style="background: white; color: red">color</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">rgba(112, 112, 112, 1)</span><span style="background: white; color: black">;
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

        </span><span style="background: white; color: maroon">.page </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">border</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">1px solid rgb(212, 212, 212)</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">100%</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">max-height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">100%</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">10px</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">position</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">relative</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: maroon">#confirm &gt; p </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">padding-bottom</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">20px</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: maroon">.k-button </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">cursor</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">pointer</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: maroon">.k-window-titlebar</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">.k-window-titlebar &gt; span </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">cursor</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">move</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">font-weight</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">bold</span><span style="background: white; color: black">;
        }
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;page&quot;&gt;
        &lt;</span><span style="background: white; color: maroon">button </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;k-button&quot; </span><span style="background: white; color: red">data-bind</span><span style="background: white; color: blue">=&quot;click: onShowClick&quot;&gt;</span><span style="background: white; color: black">Show confirm</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">button</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;confirm&quot;&gt;&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/x-kendo-template&quot; </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;confirmTemplate&quot;&gt;
        &lt;</span><span style="background: white; color: maroon">p</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">#= ConfirmText #</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">p</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">button </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;k-button&quot; </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;yesButton&quot;&gt;</span><span style="background: white; color: black">Yes</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">button</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">button </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;k-button&quot; </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;noButton&quot;&gt; </span><span style="background: white; color: black">No</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">button</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    </span><span style="background: white; color: #006400">&lt;!-- Libraries --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;//code.jquery.com/jquery-1.9.1.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;//cdn.kendostatic.com/2014.1.528/js/kendo.all.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    
    </span><span style="background: white; color: #006400">&lt;!-- Custom --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;app.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;</span></pre>


<p>&#160;</p>

<p><strong>Code</strong></p>

<pre class="code"><span style="background: white; color: blue">var </span><span style="background: white; color: black">kendo = kendo || {};

kendo.controller = (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">self = {};
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">_vm = </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">;
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">_confirm = </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">;
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">_confirmTemplate = </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">;

    self.show = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
        _confirm =  $(</span><span style="background: white; color: #a31515">&quot;#confirm&quot;</span><span style="background: white; color: black">).kendoWindow({
            title: </span><span style="background: white; color: #a31515">&quot;Delete record&quot;</span><span style="background: white; color: black">,
            visible: </span><span style="background: white; color: blue">false</span><span style="background: white; color: black">, </span><span style="background: white; color: green">// The window will not appear before its .open method is called.
            </span><span style="background: white; color: black">width: </span><span style="background: white; color: #a31515">&quot;230px&quot;</span><span style="background: white; color: black">,
            height: </span><span style="background: white; color: #a31515">&quot;100px&quot;</span><span style="background: white; color: black">,
        }).data(</span><span style="background: white; color: #a31515">&quot;kendoWindow&quot;</span><span style="background: white; color: black">);
        _confirmTemplate = kendo.template($(</span><span style="background: white; color: #a31515">&quot;#confirmTemplate&quot;</span><span style="background: white; color: black">).html());
        _vm = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">kendo.data.ObservableObject({
            onShowClick: </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
                </span><span style="background: white; color: green">// Dynamically set some window options.
                </span><span style="background: white; color: black">_confirm.setOptions({
                    position: {
                        top: 200,
                        left: 200
                    }
                });
                _confirm.content(_confirmTemplate({ ConfirmText: </span><span style="background: white; color: #a31515">&quot;Delete record?&quot;</span><span style="background: white; color: black">}));
                _confirm.open();

                $(</span><span style="background: white; color: #a31515">&quot;#yesButton&quot;</span><span style="background: white; color: black">).click(</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {

                    </span><span style="background: white; color: green">// TODO: Delete record.
                    </span><span style="background: white; color: black">_confirm.close();
                })
                $(</span><span style="background: white; color: #a31515">&quot;#noButton&quot;</span><span style="background: white; color: black">).click(</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
                    </span><span style="background: white; color: green">// User cancelled the window.
                    </span><span style="background: white; color: black">_confirm.close();
                })
            }
        });

        kendo.bind($(</span><span style="background: white; color: #a31515">&quot;.page&quot;</span><span style="background: white; color: black">), _vm);
    };

    </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">self;
})();

kendo.controller.show();</span></pre>
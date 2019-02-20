---
ID: 3871
post_title: 'MVVM &#8211; Kendo UI ListView &#8211; Get selected items on selection.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/06/26/mvvm-kendo-ui-listview-get-selected-items-on-selection/
published: true
post_date: 2014-06-26 14:59:40
---
<p>This page shows how you can get the selected items when using Kendo UI MVVM:</p>  <p>&#160;</p>  <pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">!DOCTYPE </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
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
</span><span style="background: white; color: blue">
&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;page&quot;&gt;
&lt;</span><span style="background: white; color: maroon">button </span><span style="background: white; color: red">onclick</span><span style="background: white; color: blue">=&quot;</span><span style="background: white; color: black">app.onExecuteClick(event);</span><span style="background: white; color: blue">&quot;&gt;</span><span style="background: white; color: black">Execute</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">button</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/x-kendo-tmpl&quot; </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;template&quot;&gt;
    &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;k-widget&quot;&gt;
        &lt;</span><span style="background: white; color: maroon">dl</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">dt</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">Product Name</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">dt</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">dd</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">#:ProductName#</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">dd</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">dt</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">Unit Price</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">dt</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">dd</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">#:kendo.toString(UnitPrice, &quot;c&quot;)#</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">dd</span><span style="background: white; color: blue">&gt;
        &lt;/</span><span style="background: white; color: maroon">dl</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">data-role</span><span style="background: white; color: blue">=&quot;listview&quot;
        </span><span style="background: white; color: red">data-template</span><span style="background: white; color: blue">=&quot;template&quot;
        </span><span style="background: white; color: red">data-selectable</span><span style="background: white; color: blue">=&quot;multiple&quot;
        </span><span style="background: white; color: red">data-bind</span><span style="background: white; color: blue">=&quot;source: products, events: { change: onProductChange }&quot;
        </span><span style="background: white; color: red">style</span><span style="background: white; color: blue">=&quot;</span><span style="background: white; color: red">width</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">420px</span><span style="background: white; color: black">; </span><span style="background: white; color: red">height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">200px</span><span style="background: white; color: black">; </span><span style="background: white; color: red">overflow</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">auto&quot;&gt;&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot;&gt;
var </span><span style="background: white; color: black">app = (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
{
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">self = {};

    self.onExecuteClick = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(e)
    {
        </span><span style="background: white; color: blue">debugger</span><span style="background: white; color: black">;
    };

    self.start = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(e)
    {
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">products = [
            { Id: 1, ProductName: </span><span style="background: white; color: #a31515">'Product1'</span><span style="background: white; color: black">, UnitPrice: 200 },
            { Id: 2, ProductName: </span><span style="background: white; color: #a31515">'Product2'</span><span style="background: white; color: black">, UnitPrice: 300 },
            { Id: 3, ProductName: </span><span style="background: white; color: #a31515">'Product3'</span><span style="background: white; color: black">, UnitPrice: 400 }
        ];

        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">viewModel = kendo.observable({
            selectedProducts: </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">,
            products: </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">kendo.data.DataSource({
                schema: {
                    model: {
                        id: </span><span style="background: white; color: #a31515">&quot;Id&quot;
                    </span><span style="background: white; color: black">}
                },
                data: products
            }),
            onProductChange: </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(e)
            {
                </span><span style="background: white; color: green">// Get kendo listview.
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">$listView = e.sender;
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">data = $listView.dataSource.view();

                </span><span style="background: white; color: green">// Get the selected DOM elements as jQuery objects.
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">$selectedElements = $listView.select();

                </span><span style="background: white; color: green">// Convert the selected  jQuery DOM elements to a Array containing only &quot;Product&quot; objects.
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">selected = $.map($selectedElements, </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(item)
                {
                    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">index = $(item).index();
                    </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">data[index];
                });

                </span><span style="background: white; color: green">// Log the selected products to the console.
                </span><span style="background: white; color: black">console.log(selected);
            }
        });

        kendo.bind($(</span><span style="background: white; color: #a31515">&quot;#page&quot;</span><span style="background: white; color: black">), viewModel);
    };

    </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">self;
})();

app.start();
</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;</span></pre>
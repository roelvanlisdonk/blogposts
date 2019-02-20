---
ID: 4182
post_title: >
  Creating a vertical linear gradient
  border with solid border as fallback for
  older browsers.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/12/03/creating-a-linear-gradient-border-with-solid-border-as-fallback-for-older-browsers/
published: true
post_date: 2014-12-03 14:30:18
---
<p>Code can be found here: <a title="http://plnkr.co/edit/EgLVcgyPcbu7AngvnnOy?p=preview" href="http://plnkr.co/edit/EgLVcgyPcbu7AngvnnOy?p=preview">http://plnkr.co/edit/EgLVcgyPcbu7AngvnnOy?p=preview</a></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/12/image3.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/12/image_thumb3.png" width="393" height="187" /></a></p>  <p>&#160;</p>  <pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">!DOCTYPE </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">Vanilla javascript spike page.</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">charset</span><span style="background: white; color: blue">=&quot;utf-8&quot;&gt;
    &lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">http-equiv</span><span style="background: white; color: blue">=&quot;X-UA-Compatible&quot; </span><span style="background: white; color: red">content</span><span style="background: white; color: blue">=&quot;IE=edge&quot;&gt;

    </span><span style="background: white; color: #006400">&lt;!-- App styles --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;
        </span><span style="background: white; color: maroon">html</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">body </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">100%</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: maroon">body</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">div</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">p</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">ul</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">li </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">border</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">-webkit-box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">-moz-box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">margin</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">outline</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: maroon">body </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">20px</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">background-color</span><span style="background: white; color: black">:</span><span style="background: white; color: blue">#393939</span><span style="background: white; color: black">;
        }
             
        </span><span style="background: white; color: maroon">.bordered </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">color</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">#F1F1F1</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">display</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">inline-block</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">width</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">180px</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">100px</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">border-right</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">1px solid #F1F1F1</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">border-image</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">linear-gradient(to bottom, #393939 0%,#F1F1F1 25%,#F1F1F1 75%,#393939 100%) 1 stretch</span><span style="background: white; color: black">;
        }
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;

   </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;bordered&quot;&gt;</span><span style="background: white; color: black">A linear gradient border:</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
</span></pre>
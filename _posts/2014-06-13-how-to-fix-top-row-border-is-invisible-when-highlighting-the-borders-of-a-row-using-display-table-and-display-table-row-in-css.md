---
ID: 3849
post_title: 'How to fix: top row border is invisible, when highlighting the borders of a row using display table and display table-row in CSS.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/06/13/how-to-fix-top-row-border-is-invisible-when-highlighting-the-borders-of-a-row-using-display-table-and-display-table-row-in-css/
published: true
post_date: 2014-06-13 11:15:46
---
<p>If you want to highlight the borders of a row, when using display table and display table-row, like:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/06/image9.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/06/image_thumb9.png" width="397" height="369" /></a></p>  <p>&#160;</p>  <p>You must style the row bottom, left and right borders, but for the top border you need to style the cells, otherwise the top border of the row will not show, for rows that have other rows before it.</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/06/image10.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/06/image_thumb10.png" width="402" height="379" /></a></p>  <p>&#160;</p>  <pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">!DOCTYPE </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">Basic styling research page.</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;

    &lt;</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;
        </span><span style="background: white; color: maroon">* </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">margin</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">-moz-box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">-webkit-box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: maroon">body </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">20px</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: maroon">.table </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">display</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">table</span><span style="background: white; color: black">;
            </span><span style="background: white; color: #006400">/* Show borders, when using display: table. */
            </span><span style="background: white; color: red">border-collapse</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">collapse</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: maroon">.tablerow </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">display</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">table-row</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">border</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">1px solid rgb(218, 218, 218)</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: #006400">/* Add some spacing between the first and second column. */
        </span><span style="background: white; color: maroon">.tablerow div:first-child </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">padding-right</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">10px</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: maroon">.tablecell </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">display</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">table-cell</span><span style="background: white; color: black">;
        }
        
        </span><span style="background: white; color: #006400">/* Style the bottom, left and right row borders. */
        </span><span style="background: white; color: maroon">.selected </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">border</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">1px solid #1984c8</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: #006400">/* Style the top of each cell to fake the row top border. */
        </span><span style="background: white; color: maroon">.selected div </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">border-top</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">1px solid #1984c8</span><span style="background: white; color: black">;
        }
        
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;table&quot;&gt;
        &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;tablerow&quot;&gt;
            &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;tablecell&quot;&gt;</span><span style="background: white; color: black">Cell 1.1</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;tablecell&quot;&gt;</span><span style="background: white; color: black">Cell 1.2</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
        &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;tablerow&quot;&gt;
            &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;tablecell&quot;&gt;</span><span style="background: white; color: black">Cell 2.1</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;tablecell&quot;&gt;</span><span style="background: white; color: black">Cell 2.2</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
        &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;tablerow selected&quot;&gt;
            &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;tablecell&quot;&gt;</span><span style="background: white; color: black">Cell 3.1</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;tablecell&quot;&gt;</span><span style="background: white; color: black">Cell 3.2</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
        &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;tablerow&quot;&gt;
            &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;tablecell&quot;&gt;</span><span style="background: white; color: black">Cell 4.1</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;tablecell&quot;&gt;</span><span style="background: white; color: black">Cell 4.2</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
        &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;tablerow&quot;&gt;
            &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;tablecell&quot;&gt;</span><span style="background: white; color: black">Cell 5.1</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;tablecell&quot;&gt;</span><span style="background: white; color: black">Cell 5.2</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
        &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;</span></pre>
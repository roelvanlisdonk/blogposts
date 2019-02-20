---
ID: 3854
post_title: 'Fix table-cell height overflow-y (scroll) in a CSS 3 full page 100% height layout'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/06/17/fix-table-cell-height-overflow-y-scroll-in-a-css-3-full-page-100-height-layout/
published: true
post_date: 2014-06-17 13:39:49
---
<p>&#160;</p>  <p>If you are using display: table, display: table-row and display: table-cell in CSS to structure your HTML, then restricting the height of a content cell is difficult. If you want to have a content cell scroll correctly vertically, when the content of a cell exceeds the height of the table, like cell 2 in the following screen dump:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/06/image11.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/06/image_thumb11.png" width="580" height="383" /></a></p>  <p>&#160;</p>  <p>Then you can use a “relative” positioned div inside the table-cell and in the relative positioned div a absolute positioned div. This div should get the overflow-y property, like:</p>   <pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;table&quot; </span><span style="background: white; color: red">style</span><span style="background: white; color: blue">=&quot;</span><span style="background: white; color: red">height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">100%</span><span style="background: white; color: black">;</span><span style="background: white; color: blue">&quot;&gt;
    &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;row&quot;&gt;
        &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;cell&quot; </span><span style="background: white; color: red">style</span><span style="background: white; color: blue">=&quot;</span><span style="background: white; color: red">border</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">1px solid #000000</span><span style="background: white; color: black">; </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">10px</span><span style="background: white; color: black">;</span><span style="background: white; color: blue">&quot;&gt;</span><span style="background: white; color: black">Cell 1</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;cell&quot; </span><span style="background: white; color: red">style</span><span style="background: white; color: blue">=&quot;</span><span style="background: white; color: red">border</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">1px solid #000000</span><span style="background: white; color: black">; </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">10px</span><span style="background: white; color: black">;</span><span style="background: white; color: blue">&quot;&gt;
            </span><span style="background: white; color: #006400">&lt;!-- Use inner div's with position relative and absolute, to fix cell height,
                 making it overflow correctly. --&gt;
            </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">style</span><span style="background: white; color: blue">=&quot;</span><span style="background: white; color: red">position</span><span style="background: white; color: black">:</span><span style="background: white; color: blue">relative</span><span style="background: white; color: black">; </span><span style="background: white; color: red">height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">100%&quot;&gt;
                &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">style</span><span style="background: white; color: blue">=&quot;</span><span style="background: white; color: red">overflow-y</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">scroll</span><span style="background: white; color: black">; </span><span style="background: white; color: red">position</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">absolute</span><span style="background: white; color: black">; </span><span style="background: white; color: red">top</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">; </span><span style="background: white; color: red">right</span><span style="background: white; color: black">:</span><span style="background: white; color: blue">0</span><span style="background: white; color: black">; </span><span style="background: white; color: red">bottom</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">; </span><span style="background: white; color: red">left</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;</span><span style="background: white; color: blue">&quot;&gt;

</span></pre>


<p>To see the code live: <a title="http://plnkr.co/edit/HWTsCsUpddHP3rZsMUtz?p=preview" href="http://plnkr.co/edit/HWTsCsUpddHP3rZsMUtz?p=preview">http://plnkr.co/edit/HWTsCsUpddHP3rZsMUtz?p=preview</a></p>
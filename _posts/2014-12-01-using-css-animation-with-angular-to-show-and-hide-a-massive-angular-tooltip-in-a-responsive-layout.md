---
ID: 4174
post_title: >
  Using css animation with angular, to
  show and hide a massive angular tooltip
  in a responsive layout.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/12/01/using-css-animation-with-angular-to-show-and-hide-a-massive-angular-tooltip-in-a-responsive-layout/
published: true
post_date: 2014-12-01 10:36:05
---
<p>Code can be found at:</p>  <p><a title="http://plnkr.co/edit/xarxPAKTXrEIDKUHmapg?p=preview" href="http://plnkr.co/edit/xarxPAKTXrEIDKUHmapg?p=preview">http://plnkr.co/edit/xarxPAKTXrEIDKUHmapg?p=preview</a></p>  <p>&#160;</p>  <p>I was asked to show a tooltip with AngularJS in a responsive layout, so I created a Plunker, that will form the base of my code.</p>  <p>Note: resize the screen to test the responsiveness.</p>  <p>&#160;</p>  <p><strong>Initial state</strong></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/12/image.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/12/image_thumb.png" width="580" height="299" /></a></p>  <p><strong></strong></p>  <p><strong>Clicked on Tile 3</strong></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/12/image1.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/12/image_thumb1.png" width="580" height="314" /></a></p>  <p><strong></strong></p>  <p>&#160;</p>  <p><strong>HTML</strong></p>  <pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">ng-controller</span><span style="background: white; color: blue">=&quot;main&quot;&gt;
        &lt;</span><span style="background: white; color: maroon">br</span><span style="background: white; color: blue">&gt;
        </span><span style="background: white; color: black">{{ </span><span style="background: white; color: purple">title </span><span style="background: white; color: black">}}
        </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">br</span><span style="background: white; color: blue">&gt;
        </span><span style="background: white; color: black">Just click on one of the tiles to show the tooltip.
        </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">br</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">br</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;header&quot;&gt;
            </span><span style="background: white; color: black">Modules
        </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;tiles&quot;&gt;
            &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;tile&quot; </span><span style="background: white; color: red">ng-class</span><span style="background: white; color: blue">=&quot;{ marker: tile.showToolTip }&quot;
                 </span><span style="background: white; color: red">ng-click</span><span style="background: white; color: blue">=&quot;onTileClick(tile)&quot;
                 </span><span style="background: white; color: red">ng-repeat-start</span><span style="background: white; color: blue">=&quot;tile in tiles&quot;&gt;
                </span><span style="background: white; color: black">{{ </span><span style="background: white; color: purple">tile.title </span><span style="background: white; color: black">}}
            </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;wizard fadeSlideIn&quot; </span><span style="background: white; color: red">ng-show</span><span style="background: white; color: blue">=&quot;tile.showToolTip&quot; </span><span style="background: white; color: red">ng-repeat-end</span><span style="background: white; color: blue">&gt;
                &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;close&quot;&gt;</span><span style="background: white; color: black">X</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
                &lt;</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">{{ </span><span style="background: white; color: purple">tile.title </span><span style="background: white; color: black">}}</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
                &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">style</span><span style="background: white; color: blue">=&quot;</span><span style="background: white; color: red">clear</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">both&quot;&gt;&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
            &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
        &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;

    &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;</span></pre>
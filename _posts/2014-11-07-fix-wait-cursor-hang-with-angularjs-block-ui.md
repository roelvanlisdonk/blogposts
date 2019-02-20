---
ID: 4115
post_title: 'Fix: wait cursor hang with AngularJS Block UI'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/11/07/fix-wait-cursor-hang-with-angularjs-block-ui/
published: true
post_date: 2014-11-07 15:09:20
---
<p>When I stopped Block UI the wait cursor remained until I moved the mouse.</p>  <p>To fix this problem I changed the Block UI css (I moved the “cursor: wait” from the class .block-ui-container to the class .block-ui-active):</p>  <p>&#160;</p>  <pre class="code"><span style="background: white; color: maroon">.block-ui-container </span><span style="background: white; color: black">{
  </span><span style="background: white; color: red">position</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">absolute</span><span style="background: white; color: black">;
  </span><span style="background: white; color: red">z-index</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">10000</span><span style="background: white; color: black">;
  </span><span style="background: white; color: red">top</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">; </span><span style="background: white; color: red">right</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">; </span><span style="background: white; color: red">bottom</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">; </span><span style="background: white; color: red">left</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;
  </span><span style="background: white; color: red">height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;
  </span><span style="background: white; color: red">overflow</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">hidden</span><span style="background: white; color: black">;
  </span><span style="background: white; color: red">opacity</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;
  </span><span style="background: white; color: red">filter</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">alpha(opacity=00)</span><span style="background: white; color: black">;
}

</span><span style="background: white; color: maroon">.block-ui-active </span><span style="background: white; color: black">{
    </span><span style="background: white; color: red">cursor</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">wait</span><span style="background: white; color: black">;
}</span></pre>
---
ID: 4366
post_title: >
  How to create a triangle with pure CSS
  and HTML
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/05/22/how-to-create-a-triangle-with-pure-css-and-html/
published: true
post_date: 2015-05-22 11:39:30
---
<p>This post describes in 3 examples, how you can create a triangle with pure CSS and HTML.</p> <p>&nbsp;</p> <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/05/clip_image0014.png" rel="lightbox"><img title="clip_image001[4]" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="clip_image001[4]" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/05/clip_image0014_thumb.png" width="237" height="625"></a></p> <p>&nbsp;</p><pre class="code"><span style="color: black"><strong>HTML
</strong></span><span style="color: blue">&lt;</span><span style="color: maroon">br </span><span style="color: blue">/&gt;
</span><span style="color: black">Example 1
</span><span style="color: blue">&lt;</span><span style="color: maroon">br </span><span style="color: blue">/&gt;
&lt;</span><span style="color: maroon">br </span><span style="color: blue">/&gt;
&lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">="example1"&gt;&lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;

&lt;</span><span style="color: maroon">br </span><span style="color: blue">/&gt;
</span><span style="color: black">Example 2
</span><span style="color: blue">&lt;</span><span style="color: maroon">br </span><span style="color: blue">/&gt;
&lt;</span><span style="color: maroon">br </span><span style="color: blue">/&gt;
&lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">="example2"&gt;&lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;

&lt;</span><span style="color: maroon">br </span><span style="color: blue">/&gt;
</span><span style="color: black">Example 3
</span><span style="color: blue">&lt;</span><span style="color: maroon">br </span><span style="color: blue">/&gt;
&lt;</span><span style="color: maroon">br </span><span style="color: blue">/&gt;
&lt;</span><span style="color: maroon">div </span><span style="color: red">class</span><span style="color: blue">="example3"&gt;&lt;/</span><span style="color: maroon">div</span><span style="color: blue">&gt;

</span><span style="color: black">CSS
</span><span style="color: maroon">.example1 </span><span style="color: black">{
    </span><span style="color: red">height</span><span style="color: black">: </span><span style="color: blue">40px</span><span style="color: black">;
    </span><span style="color: red">width</span><span style="color: black">: </span><span style="color: blue">40px</span><span style="color: black">;
    </span><span style="color: red">border-left</span><span style="color: black">: </span><span style="color: blue">10px solid blue</span><span style="color: black">;
    </span><span style="color: red">border-right</span><span style="color: black">: </span><span style="color: blue">10px solid blue</span><span style="color: black">;
    </span><span style="color: red">border-bottom</span><span style="color: black">: </span><span style="color: blue">10px solid #000000</span><span style="color: black">;
    </span><span style="color: red">border-top</span><span style="color: black">: </span><span style="color: blue">10px solid #000000</span><span style="color: black">;
}

</span><span style="color: maroon">.example2 </span><span style="color: black">{
    </span><span style="color: red">height</span><span style="color: black">: </span><span style="color: blue">20px</span><span style="color: black">;
    </span><span style="color: red">width</span><span style="color: black">: </span><span style="color: blue">20px</span><span style="color: black">;
    </span><span style="color: red">border-left</span><span style="color: black">: </span><span style="color: blue">10px solid blue</span><span style="color: black">;
    </span><span style="color: red">border-right</span><span style="color: black">: </span><span style="color: blue">10px solid blue</span><span style="color: black">;
    </span><span style="color: red">border-bottom</span><span style="color: black">: </span><span style="color: blue">10px solid #000000</span><span style="color: black">;
    </span><span style="color: red">border-top</span><span style="color: black">: </span><span style="color: blue">10px solid #000000</span><span style="color: black">;
}

</span><span style="color: maroon">.example3 </span><span style="color: black">{
    </span><span style="color: red">width</span><span style="color: black">: </span><span style="color: blue">0</span><span style="color: black">;
    </span><span style="color: red">height</span><span style="color: black">: </span><span style="color: blue">0</span><span style="color: black">;
    </span><span style="color: red">border-left</span><span style="color: black">: </span><span style="color: blue">5px solid transparent</span><span style="color: black">;
    </span><span style="color: red">border-right</span><span style="color: black">: </span><span style="color: blue">5px solid transparent</span><span style="color: black">;
    </span><span style="color: red">border-bottom</span><span style="color: black">: </span><span style="color: blue">5px solid #2f2f2f</span><span style="color: black">;
}
</pre></span>
---
ID: 4103
post_title: >
  Add animation on dom event, by using a
  custom directive, the AngularJS $animate
  service and the Animate.css library.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/10/31/add-animation-on-dom-event-by-using-a-custom-directive-the-angularjs-animate-service-and-the-animate-css-library/
published: true
post_date: 2014-10-31 09:22:38
---
<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/10/image9.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/10/image_thumb9.png" width="580" height="150" /></a></p>  <p>&#160;</p>  <p>Here’s is the code:</p>  <p>&#160;</p>  <p><a title="http://plnkr.co/edit/EdHyzxwLTfNRXFHj9iU1?p=preview" href="http://plnkr.co/edit/EdHyzxwLTfNRXFHj9iU1?p=preview">http://plnkr.co/edit/EdHyzxwLTfNRXFHj9iU1?p=preview</a></p>  <p>&#160;</p>  <p>Yes, yes I know this can easily be done with the standard AngularJS ngAnimate directive, but I wanted to play around with a custom directive, isolated scope and the AngularJS $animate service. So I decided to use a wobble effect from the Animate.css library on a “alarm bell”.</p>  <p>&#160;</p>  <p>The code use a css class “<strong>myWobble”</strong>, that uses a named keyframe animation from the Animate.css library, called: <strong>“wobble”</strong>.</p>  <pre class="code"><span style="background: white; color: maroon"><strong>.myWobble</strong> </span><span style="background: white; color: black">{
    </span><span style="background: white; color: red">-moz-animation</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">wobble 1s</span><span style="background: white; color: black">;
    </span><span style="background: white; color: red">-o-animation</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">wobble 1s</span><span style="background: white; color: black">;
    </span><span style="background: white; color: red">-webkit-animation</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">wobble 1s</span><span style="background: white; color: black">;
    </span><strong><span style="background: white; color: red">animation</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">wobble 1s</span></strong><span style="background: white; color: black"><strong>;</strong>
    </span><span style="background: white; color: red">-webkit-animation-fill-mode</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">both</span><span style="background: white; color: black">;
    </span><span style="background: white; color: red">-o-animation-fill-mode</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">both</span><span style="background: white; color: black">;
    </span><span style="background: white; color: red">animation-fill-mode</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">both</span><span style="background: white; color: black">;
}</span></pre>


<p>Then the custom directive “<strong>zvdz-animate</strong>” is used to start the animation on a dom event (in this case the on&#160; “<strong>click</strong>” event). The directive will add the class “myWobble” to the element, when the animation is done and the “<strong>reset</strong>” option is set to “<strong>true</strong>”, the class “myWobble” will be removed, so when the user clicks again on the element, the animation is started again. When the “reset” option is set to “<strong>false</strong>” the class will not be removed and the animation will not be fired again.</p>

<p>In some case this is what you want, but in this case not.</p>


<pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;alarmContainer&quot; </span><span style="background: white; color: red">zvdz-animate</span><span style="background: white; color: blue">=&quot;{ effects: [{ on: 'click', className: 'myWobble', reset: true }] }&quot;&gt;
    &lt;</span><span style="background: white; color: maroon">a </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;&quot; </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;fa fa-bell-o&quot;&gt;&lt;/</span><span style="background: white; color: maroon">a</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;</span></pre>
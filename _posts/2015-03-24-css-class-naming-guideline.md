---
ID: 4304
post_title: CSS class naming guideline
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/03/24/css-class-naming-guideline/
published: true
post_date: 2015-03-24 10:01:39
---
<p>Lets assume you want to create a &quot;error notification&quot; component and this component contains 2 sub components, a &quot;close button&quot; and a &quot;read more&quot; button in an application called &quot;spike&quot;, something like: </p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/03/image6.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/03/image_thumb6.png" width="580" height="138" /></a>&#160;</p>  <p>&#160;</p>  <p>How do I setup my CSS to style the component and it’s subcomponents.</p>  <p>Well I like to name components and subcomponents by what they are and try to keep the names descriptive, but short:</p>  <p>&#160;</p>  <pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">!doctype </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">Research</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">charset</span><span style="background: white; color: blue">=&quot;utf-8&quot;&gt;
    &lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">http-equiv</span><span style="background: white; color: blue">=&quot;X-UA-Compatible&quot; </span><span style="background: white; color: red">content</span><span style="background: white; color: blue">=&quot;IE=edge&quot;&gt;
    &lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">name</span><span style="background: white; color: blue">=&quot;description&quot; </span><span style="background: white; color: red">content</span><span style="background: white; color: blue">=&quot;Research page&quot;&gt;
    &lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">name</span><span style="background: white; color: blue">=&quot;viewport&quot; </span><span style="background: white; color: red">content</span><span style="background: white; color: blue">=&quot;width=device-width, initial-scale=1.0&quot;&gt;

    </span><span style="background: white; color: #006400">&lt;!-- Icons --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;shortcut icon&quot; </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;/Images/icon256x256.png&quot;&gt;
    &lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;icon&quot; </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;/Images/icon_96x96.png&quot;&gt;
    </span><span style="background: white; color: #006400">    
    &lt;!-- App styles --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;
        
        </span><span style="background: white; color: #006400">/* Class must be set on the root element of the &quot;error notification&quot; component. */
        </span><span style="background: white; color: maroon">.spike-error-notification </span><span style="background: white; color: black">{
            
        }

        </span><span style="background: white; color: #006400">/* Styling for the &quot;close button&quot;. */
        </span><span style="background: white; color: maroon">.spike-error-notification
        .spike-close-button </span><span style="background: white; color: black">{
            
        }

        </span><span style="background: white; color: #006400">/* Styling for the &quot;read-more button&quot;. */
        </span><span style="background: white; color: maroon">.spike-error-notification
        .spike-read-more-button </span><span style="background: white; color: black">{
            
        }

    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;spike-error-notification&quot;&gt;
        &lt;</span><span style="background: white; color: maroon">button </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;spike-close-button&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;button&quot;&gt;&lt;</span><span style="background: white; color: maroon">span</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">×</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">span</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: maroon">button</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">strong</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">An unhandled exception occurred.</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">strong</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">button </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;spike-read-more-button&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;button&quot;&gt;</span><span style="background: white; color: black">Read more...</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">button</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
</span></pre>
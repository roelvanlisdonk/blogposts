---
ID: 3212
post_title: >
  Wrapping the
  MSApp.execUnsafeLocalFunction
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/05/03/wrapping-the-msapp-execunsafelocalfunction/
published: true
post_date: 2013-05-03 15:53:01
---
<p>Microsoft’s MSApp.execUnsafeLocalFunction can be used to dynamically add potentially unsafe code to the DOM. If you want to use this function in a cross platform HTML 5 app, you might want to wrap the function like:</p>  <pre class="code"><span style="background: white; color: blue">if </span><span style="background: white; color: black">(</span><span style="background: white; color: #a31515">&quot;undefined&quot; </span><span style="background: white; color: black">=== </span><span style="background: white; color: blue">typeof </span><span style="background: white; color: black">Utilities)
{
    Utilities = {};
}

Utilities.executeUnsafe = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(func)
{
    </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(</span><span style="background: white; color: #a31515">&quot;undefined&quot; </span><span style="background: white; color: black">!== </span><span style="background: white; color: blue">typeof </span><span style="background: white; color: black">MSApp)
    {
        MSApp.execUnsafeLocalFunction(</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
        {
            func();
        });
    }
    </span><span style="background: white; color: blue">else
    </span><span style="background: white; color: black">{
        func();
    }
};</span></pre>

<p>Now you can call a potentially unsafe function, like:</p>

<pre class="code"><p><span style="background: white; color: black">Utilities.executeUnsafe(App.myFunction);</span></p></pre>


<p>Where App.myFunction should be replaced by your function.</p>
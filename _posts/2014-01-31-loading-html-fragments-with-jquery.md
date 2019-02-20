---
ID: 3682
post_title: Loading HTML fragments with jQuery
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/01/31/loading-html-fragments-with-jquery/
published: true
post_date: 2014-01-31 12:53:28
---
<p>When I want to load a html fragment I prefer the contents of the container div in the page and the HTML fragment to have the same ID, like:</p>  <p>&#160;</p>  <p><strong>Master page</strong></p>  <pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">!DOCTYPE </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">Master page</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
    </span><span style="background: white; color: #006400">&lt;!--Placeholder container. --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;page&quot;&gt;&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;</span></pre>



<p><strong>Page (html fragment)</strong></p>

<pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">!DOCTYPE </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">Page (html fragment)</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
    </span><span style="background: white; color: #006400">&lt;!-- Page (html fragment to load). --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;page&quot;&gt;&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;</span></pre>


<p>&#160;</p>

<p>Then the following code can be used to replace the contents of the &quot;placeholder&quot; div, by the contents of the ”html fragment&quot; div:</p>

<p>&#160;</p>

<p><strong>Code</strong></p>


<pre class="code"><span style="background: white; color: green">// Loads a html fragment.
// It replaces the content of the given DOM element, with the html fragment contents.
// It expects both the current page and the html fragment to contain the same &quot;id&quot; as the given id.
//
// Parameters:
// [id] example [&quot;#page&quot;].
// [url] example [&quot;Features/Login/LoginView.html&quot;].
</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">loadHtmlFragment (id, url)
{
    </span><span style="background: white; color: green">// Use jQuery &quot;ajax&quot; instead of jQuery &quot;load&quot;, because &quot;load&quot; will get the whole div, 
    // when used with selector &quot;#page&quot; and not the contents.
    // You can get only the contents with &quot;load&quot;, by using &quot;url #page &gt; *&quot;, 
    // but that will only get the child elements of the div, 
    // stripping out any direct child text.
    </span><span style="background: white; color: black">$.ajax({
        url: url,
        type: </span><span style="background: white; color: #a31515">'GET'</span><span style="background: white; color: black">,
        dataType: </span><span style="background: white; color: #a31515">&quot;html&quot;</span><span style="background: white; color: black">,
        success: </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(data)
        {
            </span><span style="background: white; color: green">// Strip out any javascript by using &quot;parseHtml&quot;.
            // Only use the contents of the html fragment by using &quot;html()&quot;.
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">dom = $(</span><span style="background: white; color: #a31515">&quot;&lt;div&gt;&quot;</span><span style="background: white; color: black">).append($.parseHTML(data)).find(id).html();

            </span><span style="background: white; color: green">// Adjust UI.
            </span><span style="background: white; color: black">$(id).html(dom);
        }
    });
};</span></pre>
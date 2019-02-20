---
ID: 3514
post_title: 'Combine base URL string with a relative path string in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/10/14/combine-base-url-string-with-a-relative-path-string-in-c/
published: true
post_date: 2013-10-14 14:36:06
---
<p>One way of combining a base URL string with a relative path string in C#:</p>  <p>&#160;</p>   <pre class="code"><span style="background: white; color: black">[</span><span style="background: white; color: #2b91af">TestMethod</span><span style="background: white; color: black">]
</span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Combine_base_url_with_relative_path_test()
{
    </span><span style="background: white; color: #2b91af">Char </span><span style="background: white; color: black">slash = </span><span style="background: white; color: #a31515">'/'</span><span style="background: white; color: black">;

    </span><span style="background: white; color: green">// Make sure sharePointUrl does not end with a slash.
    </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">sharePointUrl = </span><span style="background: white; color: #a31515">&quot;https://mySharePointServer/sites/mysites&quot;</span><span style="background: white; color: black">;
    </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(sharePointUrl.EndsWith(slash.ToString()))
    {
        sharePointUrl = sharePointUrl.TrimEnd(slash);
    }

    </span><span style="background: white; color: green">// Make sure templatesRelatviePath does not start with a slash.
    </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">templatesRelatviePath = </span><span style="background: white; color: #a31515">&quot;Shared Document/SubFolder1/SubFolder2&quot;</span><span style="background: white; color: black">;
    </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(templatesRelatviePath.StartsWith(slash.ToString()))
    {
        templatesRelatviePath = templatesRelatviePath.TrimEnd(slash);
    }

    </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">templateAbsolutePath = </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">&quot;{0}{1}{2}&quot;</span><span style="background: white; color: black">, sharePointUrl, slash, templatesRelatviePath);
            
    </span><span style="background: white; color: green">// Assert
    </span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">.AreEqual(</span><span style="background: white; color: #a31515">&quot;https://mySharePointServer/sites/mysites/Shared Document/SubFolder1/SubFolder2&quot;</span><span style="background: white; color: black">, 
        templateAbsolutePath);
}</span></pre>
<a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/10/image6.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/10/image_thumb6.png" width="524" height="62" /></a>
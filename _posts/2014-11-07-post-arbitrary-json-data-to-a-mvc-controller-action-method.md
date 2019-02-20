---
ID: 4111
post_title: >
  Post arbitrary JSON data to a MVC
  controller action method
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/11/07/post-arbitrary-json-data-to-a-mvc-controller-action-method/
published: true
post_date: 2014-11-07 09:51:31
---
<p>If you want to sent arbitrary JSON data to a MVC controller action method, you can use the following code:</p>  <pre class="code"><span style="background: white; color: black">[</span><span style="background: white; color: #2b91af">HttpPost</span><span style="background: white; color: black">]
</span><span style="background: white; color: blue">public </span><span style="background: white; color: #2b91af">ActionResult </span><span style="background: white; color: black">HandleRequest()
{
    </span><span style="background: white; color: green">// Read the RAW JSON from the request, 
    // because MVC does not support a dynamic input parameter or an input parameter of type JObject.
    // ASP .NET Web API does support a dynamic input parameter or an input parameter of type JObject.
    </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">json = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">StreamReader</span><span style="background: white; color: black">(</span><span style="background: white; color: blue">this</span><span style="background: white; color: black">.Request.InputStream).ReadToEnd();
    </span><span style="background: white; color: blue">dynamic </span><span style="background: white; color: black">clientData = </span><span style="background: white; color: #2b91af">JObject</span><span style="background: white; color: black">.Parse(json);</span></pre>
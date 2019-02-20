---
ID: 3516
post_title: >
  How to send correct UTF8 JSON to a Web
  Api controller
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/10/25/how-to-send-correct-utf8-json-to-a-web-api-controller/
published: true
post_date: 2013-10-25 08:13:27
---
<p>When posting UTF8 JSON data with the WebClient.UploadString function, I was getting NULL as value for the parameter on the controller function, the simple fix:</p>  <p>&#160;</p>  <pre class="code"><p><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">client = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">WebClient</span><span style="background: white; color: black">())
{
    </span><span style="background: white; color: green">// Set the header so it knows we are sending JSON.
    </span><span style="background: white; color: black">client.Headers[</span><span style="background: white; color: #2b91af">HttpRequestHeader</span><span style="background: white; color: black">.ContentType] = </span><span style="background: white; color: #a31515">&quot;application/json&quot;</span><span style="background: white; color: black">;
    client.Encoding = </span><span style="background: white; color: #2b91af">UTF8Encoding</span><span style="background: white; color: black">.UTF8;

    </span><span style="background: white; color: green">// …</span></p><p><span style="background: white; color: green"></span><span style="background: white; color: black">    </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">responseData = client.UploadString(&quot;http://localhost/service&quot;, utf8RequestData);

    </span><span style="background: white; color: green">// Deserialise the response into a object
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">outputDTO = </span><span style="background: white; color: #2b91af">JsonConvert</span><span style="background: white; color: black">.DeserializeObject&lt;</span><span style="background: white; color: #2b91af">GenerateDocumentOutputDto</span><span style="background: white; color: black">&gt;(responseData);
</span><span style="background: white; color: black">}</span></p></pre>
Or you could change the ContentType: 

<p>&#160;</p>

<p><span style="background: white; color: green"></span><span style="background: white; color: black">client.Headers[</span><span style="background: white; color: #2b91af">HttpRequestHeader</span><span style="background: white; color: black">.ContentType] = </span><span style="background: white; color: #a31515">&quot;application/json; charset=utf-8&quot;</span><span style="background: white; color: black">; </span></p>
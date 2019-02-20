---
ID: 3505
post_title: 'How to POST a string[] array to a ASP .NET Web Api REST service that uses JSON, from a .NET 2.0 assembly'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/10/09/how-to-post-a-string-array-to-a-asp-net-web-api-rest-service-that-uses-json-from-a-net-2-0-assembly/
published: true
post_date: 2013-10-09 12:07:25
---
<p>In this post I will use a UnitTest project written in C# .NET 2.0 as client code.</p>  <p>And a ASP .NET Web Api project as Server (service).</p>  <p>&#160;</p>  <h1>Client code</h1>  <p>Create a new UnitTest project and change target framework to .net 3.5.</p>  <p>Add nuget package JSON.NET.</p>  <p>&#160;</p>  <p>&#160;</p>  <p>&#160;</p>  <p>&#160;</p>  <pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">WordMerge.EndToEndTests
{
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Microsoft.VisualStudio.TestTools.UnitTesting;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Net;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Newtonsoft.Json;

    [</span><span style="background: white; color: #2b91af">TestClass</span><span style="background: white; color: black">]
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">UnitTest1
    </span><span style="background: white; color: black">{
        [</span><span style="background: white; color: #2b91af">TestMethod</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Execute_a_get_request()
        {
            </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">url = </span><span style="background: white; color: #a31515">&quot;http://localhost:63544/api/document&quot;</span><span style="background: white; color: black">;
            </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">result = </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Empty;

            </span><span style="background: white; color: green">// Uses the System.Net.WebClient and not HttpClient, because .NET 2.0 must be supported.
            </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">client = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">WebClient</span><span style="background: white; color: black">())
            {
                </span><span style="background: white; color: green">// Set the header so it knows we are requesting JSON.
                </span><span style="background: white; color: black">client.Headers[</span><span style="background: white; color: #2b91af">HttpRequestHeader</span><span style="background: white; color: black">.ContentType] = </span><span style="background: white; color: #a31515">&quot;application/json&quot;</span><span style="background: white; color: black">;

                result = client.DownloadString(url);
            }
            </span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">.AreEqual(</span><span style="background: white; color: #a31515">@&quot;[&quot;&quot;value1&quot;&quot;,&quot;&quot;value2&quot;&quot;]&quot;</span><span style="background: white; color: black">, result);
        }


        [</span><span style="background: white; color: #2b91af">TestMethod</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Execute_a_post_request()
        {
            </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">url = </span><span style="background: white; color: #a31515">&quot;http://localhost:63544/api/document&quot;</span><span style="background: white; color: black">;
            </span><span style="background: white; color: blue">object </span><span style="background: white; color: black">result = </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Empty;

            </span><span style="background: white; color: green">// Uses the System.Net.WebClient and not HttpClient, because .NET 2.0 must be supported.
            </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">client = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">WebClient</span><span style="background: white; color: black">())
            {
                </span><span style="background: white; color: green">// Set the header so it knows we are sending JSON.
                </span><span style="background: white; color: black">client.Headers[</span><span style="background: white; color: #2b91af">HttpRequestHeader</span><span style="background: white; color: black">.ContentType] = </span><span style="background: white; color: #a31515">&quot;application/json&quot;</span><span style="background: white; color: black">;

                </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">[] data = </span><span style="background: white; color: blue">new string</span><span style="background: white; color: black">[] { </span><span style="background: white; color: #a31515">&quot;This&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot; is&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot; test&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot; input&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot; data.&quot; </span><span style="background: white; color: black">};

                </span><span style="background: white; color: green">// Serialise the data we are sending in to JSON
                </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">serialisedData = </span><span style="background: white; color: #2b91af">JsonConvert</span><span style="background: white; color: black">.SerializeObject(data);

                </span><span style="background: white; color: green">// Make the request
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">response = client.UploadString(url, serialisedData);

                </span><span style="background: white; color: green">// Deserialise the response into a GUID
                </span><span style="background: white; color: black">result = </span><span style="background: white; color: #2b91af">JsonConvert</span><span style="background: white; color: black">.DeserializeObject(response);
            }

            </span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">.AreEqual(</span><span style="background: white; color: #a31515">@&quot;Succesfully uploaded: This, is, test, input, data.&quot;</span><span style="background: white; color: black">, result.ToString());
        }
    }
}
</span></pre>


<p><strong>NuGet packages config</strong></p>

<p>&#160;</p>

<pre class="code"><span style="background: white; color: blue">&lt;?</span><span style="background: white; color: #a31515">xml </span><span style="background: white; color: red">version</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">1.0</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">encoding</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">utf-8</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">?&gt;
&lt;</span><span style="background: white; color: #a31515">packages</span><span style="background: white; color: blue">&gt;
  &lt;</span><span style="background: white; color: #a31515">package </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">Newtonsoft.Json</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">version</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">5.0.6</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">targetFramework</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">net35</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: blue">/&gt;
&lt;/</span><span style="background: white; color: #a31515">packages</span><span style="background: white; color: blue">&gt;</span></pre>


<h1>Server (service) code</h1>

<p>Create an empty ASP .NET Web API project in Microsoft Visual Studio 2013.</p>

<pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">Service.api
{
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Collections.Generic;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Linq;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Net;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Net.Http;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Web.Http;

    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">DocumentController </span><span style="background: white; color: black">: </span><span style="background: white; color: #2b91af">ApiController
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: green">// GET api/&lt;controller&gt;
        </span><span style="background: white; color: blue">public </span><span style="background: white; color: #2b91af">IEnumerable</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt; Get()
        {
            </span><span style="background: white; color: blue">return new string</span><span style="background: white; color: black">[] { </span><span style="background: white; color: #a31515">&quot;value1&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;value2&quot; </span><span style="background: white; color: black">};
        }

        </span><span style="background: white; color: green">// GET api/&lt;controller&gt;/5
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">Get(</span><span style="background: white; color: blue">int </span><span style="background: white; color: black">id)
        {
            </span><span style="background: white; color: blue">return </span><span style="background: white; color: #a31515">&quot;value&quot;</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: green">// POST api/&lt;controller&gt;
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">Post([</span><span style="background: white; color: #2b91af">FromBody</span><span style="background: white; color: black">]</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">[] values)
        {
            </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">seperator = </span><span style="background: white; color: #a31515">&quot;,&quot;</span><span style="background: white; color: black">;
            </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">data = </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Join(seperator,values.ToList&lt;</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt;());
            </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">result = </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">&quot;Succesfully uploaded: {0}&quot;</span><span style="background: white; color: black">, data);
            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">result;
        }

        </span><span style="background: white; color: green">// PUT api/&lt;controller&gt;/5
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Put(</span><span style="background: white; color: blue">int </span><span style="background: white; color: black">id, [</span><span style="background: white; color: #2b91af">FromBody</span><span style="background: white; color: black">]</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">value)
        {
        }

        </span><span style="background: white; color: green">// DELETE api/&lt;controller&gt;/5
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Delete(</span><span style="background: white; color: blue">int </span><span style="background: white; color: black">id)
        {
        }
    }
}</span></pre>


<p><strong>Visual Studio Structure</strong></p>

<p><strong></strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/10/image5.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/10/image_thumb5.png" width="244" height="244" /></a></p>

<p><strong></strong></p>

<p><strong></strong></p>

<p><strong>NuGet packages config</strong></p>

<pre class="code"><span style="background: white; color: blue">&lt;?</span><span style="background: white; color: #a31515">xml </span><span style="background: white; color: red">version</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">1.0</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">encoding</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">utf-8</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">?&gt;
&lt;</span><span style="background: white; color: #a31515">packages</span><span style="background: white; color: blue">&gt;
  &lt;</span><span style="background: white; color: #a31515">package </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">Microsoft.AspNet.WebApi</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">version</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">5.0.0-rc1</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">targetFramework</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">net45</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: blue">/&gt;
  &lt;</span><span style="background: white; color: #a31515">package </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">Microsoft.AspNet.WebApi.Client</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">version</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">5.0.0-rc1</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">targetFramework</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">net45</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: blue">/&gt;
  &lt;</span><span style="background: white; color: #a31515">package </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">Microsoft.AspNet.WebApi.Core</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">version</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">5.0.0-rc1</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">targetFramework</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">net45</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: blue">/&gt;
  &lt;</span><span style="background: white; color: #a31515">package </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">Microsoft.AspNet.WebApi.WebHost</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">version</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">5.0.0-rc1</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">targetFramework</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">net45</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: blue">/&gt;
  &lt;</span><span style="background: white; color: #a31515">package </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">Newtonsoft.Json</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">version</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">4.5.11</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">targetFramework</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">net45</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: blue">/&gt;
&lt;/</span><span style="background: white; color: #a31515">packages</span><span style="background: white; color: blue">&gt;</span></pre>
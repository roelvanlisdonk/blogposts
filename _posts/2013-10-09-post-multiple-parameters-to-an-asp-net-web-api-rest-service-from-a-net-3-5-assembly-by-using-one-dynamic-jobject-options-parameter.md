---
ID: 3508
post_title: 'POST multiple parameters to an ASP .NET Web Api REST service from a .NET 3.5 assembly, by using one dynamic JObject &quot;options&quot; parameter.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/10/09/post-multiple-parameters-to-an-asp-net-web-api-rest-service-from-a-net-3-5-assembly-by-using-one-dynamic-jobject-options-parameter/
published: true
post_date: 2013-10-09 14:21:00
---
<p>&#160;</p>  <h2>Client code in .NET 3.5</h2>   <p>&#160;</p>  <pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">WordMerge.EndToEndTests
{
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Microsoft.VisualStudio.TestTools.UnitTesting;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Net;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Newtonsoft.Json;

    [</span><span style="background: white; color: #2b91af">TestClass</span><span style="background: white; color: black">]
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">UnitTest1
    </span><span style="background: white; color: black">{
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

                </span><span style="background: white; color: green">// Create the one and only &quot;options&quot; parameter object.
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">dto = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">DocumentDto
                </span><span style="background: white; color: black">{
                    TemplatePath = </span><span style="background: white; color: #a31515">@&quot;C:\Temp\Templates&quot;</span><span style="background: white; color: black">,
                    DestinationPath = </span><span style="background: white; color: #a31515">@&quot;C:\Temp\Destination&quot;</span><span style="background: white; color: black">,
                    Data = </span><span style="background: white; color: blue">new string</span><span style="background: white; color: black">[] { </span><span style="background: white; color: #a31515">&quot;This&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot; is&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot; test&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot; input&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot; data.&quot; </span><span style="background: white; color: black">}
                };

                </span><span style="background: white; color: green">// Serialise the data we are sending in to JSON
                </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">serialisedData = </span><span style="background: white; color: #2b91af">JsonConvert</span><span style="background: white; color: black">.SerializeObject(dto);

                </span><span style="background: white; color: green">// Make the request
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">response = client.UploadString(url, serialisedData);

                </span><span style="background: white; color: green">// Deserialise the response into a GUID
                </span><span style="background: white; color: black">result = </span><span style="background: white; color: #2b91af">JsonConvert</span><span style="background: white; color: black">.DeserializeObject(response);
            }

            </span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">.AreEqual(</span><span style="background: white; color: #a31515">@&quot;Succesfully uploaded: This, is, test, input, data.&quot;</span><span style="background: white; color: black">, result.ToString());
        }
    }

    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">DocumentDto
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">TemplatePath { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">DestinationPath { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">public string</span><span style="background: white; color: black">[] Data { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
    }
}
</span></pre>


<h2>Server code in .NET 4.5</h2>

<p>&#160;</p>

<p>&#160;</p>


<pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">Service.api
{
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Newtonsoft.Json.Linq;
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
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">Post([</span><span style="background: white; color: #2b91af">FromBody</span><span style="background: white; color: black">]</span><span style="background: white; color: #2b91af">JObject </span><span style="background: white; color: black">jsonData)
        {
            </span><span style="background: white; color: green">// Convert the dynamic JObject to a DocumentDto object.
            </span><span style="background: white; color: #2b91af">DocumentDto </span><span style="background: white; color: black">dto = jsonData.ToObject&lt;</span><span style="background: white; color: #2b91af">DocumentDto</span><span style="background: white; color: black">&gt;();
            
            </span><span style="background: white; color: green">// Use the given data to create the result.
            </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">seperator = </span><span style="background: white; color: #a31515">&quot;,&quot;</span><span style="background: white; color: black">;
            </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">data = </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Join(seperator, dto.Data.ToList&lt;</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">&gt;());
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

    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">DocumentDto
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">TemplatePath { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">DestinationPath { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        </span><span style="background: white; color: blue">public string</span><span style="background: white; color: black">[] Data { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
    }
}</span></pre>
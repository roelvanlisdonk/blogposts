---
ID: 3287
post_title: 'Kendo UI &ndash; jQuery and dataSource&ndash;transport&ndash;contentType'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/06/26/kendo-uijquery-and-datasourcetransportcontenttype/
published: true
post_date: 2013-06-26 14:20:51
---
<p>The way a kendo datasource retrieves data can be configured via the transport object.</p>  <p>This object contains configuration objects for specifying the way CRUD operations are executed.</p>  <p>Each of these configuration objects contain the properties</p>  <p>contentType (Type of the HTTP request)</p>  <p>dataType (Type of the HTTP response request)</p>  <p>&#160;</p>  <p>The way you configure these properties defines the way how the C# REST Service code must be written. If you use the default contentType (application/x-www-form-urlencoded; charset=UTF-8). the data is sent inside the forms collection with the name &quot;models&quot; of the request, the name of this property is set in the parameterMap function:</p>  <pre class="code"><span style="background: white; color: blue">var </span><span style="background: white; color: black">dataSource = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">kendo.data.DataSource({
    transport: {
        update: {
            </span><span style="background: white; color: green">// The default HTTP request (send) type.
            </span><span style="background: white; color: black">contentType: </span><span style="background: white; color: #a31515">&quot;application/x-www-form-urlencoded; charset=UTF-8&quot;</span><span style="background: white; color: black">,
            </span><span style="background: white; color: green">// The expected HTTP response (receive) type.
            </span><span style="background: white; color: black">dataType: </span><span style="background: white; color: #a31515">&quot;json&quot;    
        </span><span style="background: white; color: black">}
    },
    parameterMap: </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(options, operation) {
        </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(operation !== </span><span style="background: white; color: #a31515">&quot;read&quot; </span><span style="background: white; color: black">&amp;&amp; options.models) {
            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">{ models: JSON.stringify(options.models) };
        }
    }
});</span></pre>


<p>C# code to handle this update request:</p>

<pre class="code"><span style="background: white; color: blue">public </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">MyDto</span><span style="background: white; color: black">&gt; Post()
{
</span><span style="background: white; color: blue">    string </span><span style="background: white; color: black">json = _request[</span><span style="background: white; color: #a31515">&quot;models&quot;</span><span style="background: white; color: black">];
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">records = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">MyDto</span><span style="background: white; color: black">&gt;();
    </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(!</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.IsNullOrWhiteSpace(json))
    {
        records = </span><span style="background: white; color: #2b91af">JsonConvert</span><span style="background: white; color: black">.DeserializeObject&lt;</span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">MyDto</span><span style="background: white; color: black">&gt;&gt;(json);
        // Update data in database …
    }

    </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">records;
}</span></pre>


<p>MyDto is just a POCO class.</p>

<p>&#160;</p>

<p>If you want to sent the data as a parameter of the Post method, you should use &quot;contentType:&quot;application/json&quot;&quot;:</p>

<pre class="code"><span style="background: white; color: blue">var </span><span style="background: white; color: black">dataSource = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">kendo.data.DataSource({
    transport: {
        update: {
            </span><span style="background: white; color: green">// The default HTTP request (send) type.
            </span><span style="background: white; color: black">contentType: </span><span style="background: white; color: #a31515">&quot;application/json&quot;</span><span style="background: white; color: black">,
            </span><span style="background: white; color: green">// The expected HTTP response (receive) type.
            </span><span style="background: white; color: black">dataType: </span><span style="background: white; color: #a31515">&quot;json&quot;    
        </span><span style="background: white; color: black">}
    },
    parameterMap: </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(options, operation) {
        </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(operation !== </span><span style="background: white; color: #a31515">&quot;read&quot; </span><span style="background: white; color: black">&amp;&amp; options.models) {
            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">{ models: JSON.stringify(options.models) };
        }
    }
});</span></pre>


<p>C# code to handle this update request:</p>

<pre class="code"><span style="background: white; color: blue">public </span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">MyDto</span><span style="background: white; color: black">&gt; Post(</span><span style="background: white; color: #2b91af">List</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">MyDto</span><span style="background: white; color: black">&gt; records)
{
    </span><span style="background: white; color: green">// Update records in database ...

    </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">records;
}</span></pre>
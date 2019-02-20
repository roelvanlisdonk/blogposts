---
ID: 3691
post_title: >
  How to combine synchronous and
  asynchronous JavaScript function calls
  for getting data from client side cache
  or REST service (with jQuery).
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/02/21/how-to-combine-synchronous-and-asynchronous-javascript-function-calls-for-getting-data-from-client-side-cache-or-rest-service-with-jquery/
published: true
post_date: 2014-02-21 15:37:03
---
<p>&#160;</p>  <p>&#160;</p>  <p>When the user clicks on the &quot;Execute&quot; button for the first time, the data will be retrieved from a REST service.</p>  <p>The second time the data will be retrieved from the cache.</p>   <p>&#160;</p>  <p>The comments in the code will explain, how the we can return a manual promise, when data is retrieved from cache and a Ajax promise, when the data is retrieved from a REST service.</p>  <p>&#160;</p>  <pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">!DOCTYPE </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">Research page for jQuery.</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">style </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot;&gt;
    
    &lt;/</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;page&quot;&gt;
        &lt;</span><span style="background: white; color: maroon">button </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;executeButton&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;button&quot;&gt;</span><span style="background: white; color: black">Execute</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">button</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;../../Libraries/jQuery/jquery-1.10.2.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot;&gt;
        </span><span style="background: white; color: #a31515">&quot;use strict&quot;</span><span style="background: white; color: black">;


        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">cacheFactory = (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">CacheComponent = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
            {
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">self = </span><span style="background: white; color: blue">this</span><span style="background: white; color: black">;
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">_cache = {};

                </span><span style="background: white; color: green">// Returns a promise.
                // De &quot;.done&quot; function of this promise can be used to get to the data.
                </span><span style="background: white; color: black">self.getItem = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(key)
                {
                    </span><span style="background: white; color: green">// Check if key exists in de cache.
                    </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(_cache.hasOwnProperty(key))
                    {
                        </span><span style="background: white; color: green">// Get value from cache.
                        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">value = _cache[key];

                        </span><span style="background: white; color: green">// Create a manual promise.
                        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">deferred = $.Deferred();

                        </span><span style="background: white; color: green">// Imediatly set the manual promise to &quot;completed&quot;, any done functions added to the resulting promise, will be called immediately.
                        </span><span style="background: white; color: black">deferred.resolve(value);

                        </span><span style="background: white; color: green">// Data in cache, so return a manual promise.
                        </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">deferred.promise();
                    }
                    </span><span style="background: white; color: blue">else
                    </span><span style="background: white; color: black">{
                        </span><span style="background: white; color: green">// No data in cache, so return ajax promise.
                        </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">$.ajax({
                            url: key,
                            type: </span><span style="background: white; color: #a31515">&quot;GET&quot;
                        </span><span style="background: white; color: black">}).done(</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(data)
                        {
                            </span><span style="background: white; color: green">// Put the data from the service in the cache and for the purpose of demonstration add some text, 
                            // to show the difference between data from the service and data from the cache.
                            </span><span style="background: white; color: black">_cache[key] = data + </span><span style="background: white; color: #a31515">&quot; Data from cache!&quot;</span><span style="background: white; color: black">;
                        });
                    }
                };
            };

            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">_factory = {};
            _factory.create = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
            {
                </span><span style="background: white; color: green">// Create a new cache object.
                </span><span style="background: white; color: blue">return new </span><span style="background: white; color: black">CacheComponent();
            };

            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">_factory;
        })();



        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">app = (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">self = {};
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">_serviceUrl = </span><span style="background: white; color: #a31515">&quot;/Api/Service&quot;</span><span style="background: white; color: black">;

            </span><span style="background: white; color: green">// Create a new cache object by calling the &quot;create&quot; function on the &quot;cacheFactory&quot;.
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">_serviceCache = cacheFactory.create();
            
            </span><span style="background: white; color: green">// Click eventhandler.
            </span><span style="background: white; color: black">self.handleExecuteButtonClick = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(event)
            {
                
                _serviceCache
                    .getItem(_serviceUrl) </span><span style="background: white; color: green">// Get data.
                    </span><span style="background: white; color: black">.done(</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(data)
                    {
                        </span><span style="background: white; color: green">// Show data.
                        </span><span style="background: white; color: black">console.log(data);
                    });
            };

            </span><span style="background: white; color: green">// Fires when the application starts.
            </span><span style="background: white; color: black">self.start = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
            {
                console.log(</span><span style="background: white; color: #a31515">&quot;Document ready!&quot;</span><span style="background: white; color: black">);

                </span><span style="background: white; color: green">// Wire up a &quot;click&quot; evenhandler.
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">$executeButton = $(</span><span style="background: white; color: #a31515">&quot;#executeButton&quot;</span><span style="background: white; color: black">);
                $executeButton.on(</span><span style="background: white; color: #a31515">&quot;click&quot;</span><span style="background: white; color: black">, self.handleExecuteButtonClick);
            };

            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">self;
        })();

        </span><span style="background: white; color: green">// Start the application.
        </span><span style="background: white; color: black">app.start();

    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
</span></pre>


<p>&#160;</p>

<p>&#160;</p>

<p>&#160;</p>

<p>The Web API 2 routes used:</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/02/image.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/02/image_thumb.png" width="540" height="370" /></a></p>

<p>&#160;</p>

<p>The Web API 2 controller:</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/02/image1.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/02/image_thumb1.png" width="580" height="251" /></a></p>

<p>&#160;</p>

<p><strong>Result</strong></p>

<p>&#160;</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/02/image2.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/02/image_thumb2.png" width="580" height="304" /></a></p>
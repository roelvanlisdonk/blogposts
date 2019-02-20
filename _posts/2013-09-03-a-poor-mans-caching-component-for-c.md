---
ID: 3354
post_title: 'A poor man&#8217;s caching component for C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/09/03/a-poor-mans-caching-component-for-c/
published: true
post_date: 2013-09-03 16:22:50
---
<p>I needed a simple caching component that could be passed around in my code and should be thread safe.</p>  <p align="left">This is what I came up with (ps the code can be found on mine PTB project GitHub page <a href="https://github.com/roelvanlisdonk/PTB">https://github.com/roelvanlisdonk/PTB</a>):</p>  <p align="left">I you really want to do some fancy caching check out the Azure caching service:</p>  <p align="left"><a href="http://weblogs.asp.net/scottgu/archive/2013/09/03/windows-azure-new-distributed-dedicated-high-performance-cache-service-more-cool-improvements.aspx">http://weblogs.asp.net/scottgu/archive/2013/09/03/windows-azure-new-distributed-dedicated-high-performance-cache-service-more-cool-improvements.aspx</a></p>  <p align="left">&#160;</p>  <pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">PTB.Cs.Components
{
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Collections.Concurrent;

    </span><span style="background: white; color: gray">/// &lt;summary&gt;
    /// </span><span style="background: white; color: green">Holds cached data.
    </span><span style="background: white; color: gray">/// &lt;/summary&gt;
    </span><span style="background: white; color: blue">public interface </span><span style="background: white; color: #2b91af">ICacheComponent
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">Adds the given data to the cache (with a key based on the given type), if it does not exist.
        </span><span style="background: white; color: gray">/// </span><span style="background: white; color: green">Updates the data in the cache (with a key based on the given type), if it does exists.
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        </span><span style="background: white; color: blue">void </span><span style="background: white; color: black">AddOrUpdateCache&lt;T&gt;(T value);
        </span><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">Gets cached data base on the given type.
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        </span><span style="background: white; color: black">T GetCachedData&lt;T&gt;();
        </span><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">Gets cached data base on the given type, if the key is not found, the given func is executed to get the data.
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        </span><span style="background: white; color: black">T GetCachedData&lt;T&gt;(</span><span style="background: white; color: #2b91af">Func</span><span style="background: white; color: black">&lt;T&gt; getData);
        </span><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">Gets cached data base on the given type, if the key is not found, the given func is executed to get the data.
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        </span><span style="background: white; color: black">T GetCachedData&lt;K,T&gt;(</span><span style="background: white; color: #2b91af">Func</span><span style="background: white; color: black">&lt;K,T&gt; getData, K parameter);
        </span><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">Resets all cached data, by setting it to null.
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        </span><span style="background: white; color: blue">void </span><span style="background: white; color: black">ResetCache(</span><span style="background: white; color: #2b91af">ConcurrentDictionary</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">Type</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">object</span><span style="background: white; color: black">&gt; cache = </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">);
        </span><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">Resets cache for a specific item.
        </span><span style="background: white; color: gray">/// </span><span style="background: white; color: green">By setting it's value to the default of the given type.
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        </span><span style="background: white; color: blue">void </span><span style="background: white; color: black">ResetCache&lt;T&gt;();
    }

    </span><span style="background: white; color: gray">/// &lt;summary&gt;
    /// </span><span style="background: white; color: green">Holds cached data.
    </span><span style="background: white; color: gray">/// &lt;/summary&gt;
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">CacheComponent </span><span style="background: white; color: black">: </span><span style="background: white; color: #2b91af">ICacheComponent
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">Holds all cached data (thread safe).
        </span><span style="background: white; color: gray">/// </span><span style="background: white; color: green">It is declared as static readonly, so it will be initialised only once per appdomain and will never be null.
        </span><span style="background: white; color: gray">/// </span><span style="background: white; color: green">In this case it is not a problem that is always created (lazy loading is not needed here).
        </span><span style="background: white; color: gray">/// </span><span style="background: white; color: green">Using a static readonly variable ensure thread safety.
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        </span><span style="background: white; color: blue">private static readonly </span><span style="background: white; color: #2b91af">ConcurrentDictionary</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">Type</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">object</span><span style="background: white; color: black">&gt; _cache = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">ConcurrentDictionary</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">Type</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">object</span><span style="background: white; color: black">&gt;();

        </span><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">Constructor
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        </span><span style="background: white; color: blue">public </span><span style="background: white; color: black">CacheComponent()
            : </span><span style="background: white; color: blue">this</span><span style="background: white; color: black">(</span><span style="background: white; color: blue">null</span><span style="background: white; color: black">)
        {
        }

        </span><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">Added for testability.
        </span><span style="background: white; color: gray">/// </span><span style="background: white; color: green">Uses the ResetCache function to reset the cache, when needed.
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        </span><span style="background: white; color: blue">public </span><span style="background: white; color: black">CacheComponent(</span><span style="background: white; color: #2b91af">ConcurrentDictionary</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">Type</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">object</span><span style="background: white; color: black">&gt; cache)
        {
            </span><span style="background: white; color: green">// Cache alleen resestten, indien de meegegeven cache niet leeg is.
            </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(cache != </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">)
            {
                ResetCache(cache);
            }
        }

        </span><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">Adds the given data to the cache (with a key based on the given type), if it does not exist.
        </span><span style="background: white; color: gray">/// </span><span style="background: white; color: green">Updates the data in the cache (with a key based on the given type), if it does exists.
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">AddOrUpdateCache&lt;T&gt;(T value)
        {
            </span><span style="background: white; color: blue">object </span><span style="background: white; color: black">updatedValue = _cache.AddOrUpdate(</span><span style="background: white; color: blue">typeof</span><span style="background: white; color: black">(T), value, (x, existingVal) =&gt; { existingVal = value; </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">existingVal; });
        }

        </span><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">Gets cached data base on the given type.
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        </span><span style="background: white; color: blue">public </span><span style="background: white; color: black">T GetCachedData&lt;T&gt;()
        {
            </span><span style="background: white; color: blue">object </span><span style="background: white; color: black">result;
            </span><span style="background: white; color: blue">bool </span><span style="background: white; color: black">succeeded = _cache.TryGetValue(</span><span style="background: white; color: blue">typeof</span><span style="background: white; color: black">(T), </span><span style="background: white; color: blue">out </span><span style="background: white; color: black">result);
            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">(T)result;
        }

        </span><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">Gets cached data base on the given type, if the key is not found, the given func is executed to get the data and this data will be stored in the cache.
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        </span><span style="background: white; color: blue">public </span><span style="background: white; color: black">T GetCachedData&lt;T&gt;(</span><span style="background: white; color: #2b91af">Func</span><span style="background: white; color: black">&lt;T&gt; getData)
        {
            T cachedItem = GetCachedData&lt;T&gt;();
            </span><span style="background: white; color: blue">if</span><span style="background: white; color: black">(cachedItem == </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">)
            {
                cachedItem = getData();
                AddOrUpdateCache(cachedItem);
            }
            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">cachedItem;
        }

        </span><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">Gets cached data base on the given type, if the key is not found, the given func is executed with the given parameter to get the data and this data will be stored in the cache.
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        </span><span style="background: white; color: blue">public </span><span style="background: white; color: black">T GetCachedData&lt;K, T&gt;(</span><span style="background: white; color: #2b91af">Func</span><span style="background: white; color: black">&lt;K, T&gt; getData, K parameter)
        {
            T cachedItem = GetCachedData&lt;T&gt;();
            </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(cachedItem == </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">)
            {
                cachedItem = getData(parameter);
                AddOrUpdateCache(cachedItem);
            }
            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">cachedItem;
        }

        </span><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">This function is added for testability and return the total count of cached items.
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        /// &lt;returns&gt;&lt;/returns&gt;
        </span><span style="background: white; color: blue">public int </span><span style="background: white; color: black">Count()
        {
            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">_cache.Count;
        }

        </span><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">Resets all cached data, by clearing the current cache or using the given cache, when this given cache is not null.
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">ResetCache(</span><span style="background: white; color: #2b91af">ConcurrentDictionary</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">Type</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">object</span><span style="background: white; color: black">&gt; cache = </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">)
        {
            </span><span style="background: white; color: green">// Clear current cache.
            </span><span style="background: white; color: black">_cache.Clear();

            </span><span style="background: white; color: green">// Gebruik alleen de meegegeven cache, indien die niet leeg is.
            </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(cache != </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">)
            {
                </span><span style="background: white; color: blue">foreach </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">item </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">cache)
                {
                    </span><span style="background: white; color: blue">bool </span><span style="background: white; color: black">succeeded = _cache.TryAdd(item.Key, item.Value);
                    </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(!succeeded)
                    {
                        </span><span style="background: white; color: blue">throw new </span><span style="background: white; color: #2b91af">ApplicationException</span><span style="background: white; color: black">(</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">&quot;Could not add item with key [{0}] and value [{1}]&quot;</span><span style="background: white; color: black">, item.Key, item.Value));
                    }
                }
            }
        }

        </span><span style="background: white; color: gray">/// &lt;summary&gt;
        /// </span><span style="background: white; color: green">Resets cache for a specific item.
        </span><span style="background: white; color: gray">/// </span><span style="background: white; color: green">By setting it's value to the default of the given type.
        </span><span style="background: white; color: gray">/// &lt;/summary&gt;
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">ResetCache&lt;T&gt;()
        {
            AddOrUpdateCache&lt;T&gt;(</span><span style="background: white; color: blue">default</span><span style="background: white; color: black">(T));
        }
    }
}
</span></pre>

<p>&#160;</p>

<p>&#160;</p>

<pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">PTB.Cs.Test.Components
{
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">PTB.Cs.Components;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Xunit;

    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">CacheComponentTester
    </span><span style="background: white; color: black">{
        [</span><span style="background: white; color: #2b91af">Fact</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Getting_non_existing_key_should_return_null()
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">cache = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">CacheComponent</span><span style="background: white; color: black">();
            cache.ResetCache();

            </span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">.Equal(</span><span style="background: white; color: blue">null</span><span style="background: white; color: black">, cache.GetCachedData&lt;</span><span style="background: white; color: #2b91af">TypeForTesting</span><span style="background: white; color: black">&gt;());
        }

        [</span><span style="background: white; color: #2b91af">Fact</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Getting_non_existing_key_with_func_should_return_correct_value_and_data_must_be_stored_in_cache()
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">cache = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">CacheComponent</span><span style="background: white; color: black">();
            cache.ResetCache();

            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">expectedTypeForTesting = GetDataWithoutParameter();
            </span><span style="background: white; color: #2b91af">TypeForTesting </span><span style="background: white; color: black">result = cache.GetCachedData(GetDataWithoutParameter);
            </span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">.Equal(expectedTypeForTesting.Id, result.Id);
            result = cache.GetCachedData&lt;</span><span style="background: white; color: #2b91af">TypeForTesting</span><span style="background: white; color: black">&gt;();
            </span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">.Equal(expectedTypeForTesting.Id, result.Id);

            cache.ResetCache();
            result = cache.GetCachedData(GetDataWithParameter, 100);
            </span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">.Equal(expectedTypeForTesting.Id, result.Id);
            result = cache.GetCachedData&lt;</span><span style="background: white; color: #2b91af">TypeForTesting</span><span style="background: white; color: black">&gt;();
            </span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">.Equal(expectedTypeForTesting.Id, result.Id);
        }

        [</span><span style="background: white; color: #2b91af">Fact</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Getting_existing_key_should_return_correct_value()
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">cache = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">CacheComponent</span><span style="background: white; color: black">();
            cache.ResetCache();

            </span><span style="background: white; color: blue">int </span><span style="background: white; color: black">expectedInt = 100;
            cache.AddOrUpdateCache&lt;</span><span style="background: white; color: blue">int</span><span style="background: white; color: black">&gt;(expectedInt);
            </span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">.Equal(expectedInt, cache.GetCachedData&lt;</span><span style="background: white; color: blue">int</span><span style="background: white; color: black">&gt;());

            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">expectedTypeForTesting = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">TypeForTesting </span><span style="background: white; color: black">{ Id = expectedInt };
            cache.AddOrUpdateCache&lt;</span><span style="background: white; color: #2b91af">TypeForTesting</span><span style="background: white; color: black">&gt;(expectedTypeForTesting);
            </span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">.Equal(expectedTypeForTesting.Id, cache.GetCachedData&lt;</span><span style="background: white; color: #2b91af">TypeForTesting</span><span style="background: white; color: black">&gt;().Id);
        }

        [</span><span style="background: white; color: #2b91af">Fact</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Adding_multiple_items_with_same_key_should_result_in_one_cached_item()
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">cache = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">CacheComponent</span><span style="background: white; color: black">();
            cache.ResetCache();

            </span><span style="background: white; color: blue">int </span><span style="background: white; color: black">expectedInt = 100;
            cache.AddOrUpdateCache&lt;</span><span style="background: white; color: blue">int</span><span style="background: white; color: black">&gt;(expectedInt);
            cache.AddOrUpdateCache&lt;</span><span style="background: white; color: blue">int</span><span style="background: white; color: black">&gt;(expectedInt);
            cache.AddOrUpdateCache&lt;</span><span style="background: white; color: blue">int</span><span style="background: white; color: black">&gt;(expectedInt);
            cache.AddOrUpdateCache&lt;</span><span style="background: white; color: blue">int</span><span style="background: white; color: black">&gt;(expectedInt);
            cache.AddOrUpdateCache&lt;</span><span style="background: white; color: blue">int</span><span style="background: white; color: black">&gt;(expectedInt);
            cache.AddOrUpdateCache&lt;</span><span style="background: white; color: blue">int</span><span style="background: white; color: black">&gt;(expectedInt);
            
            </span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">.Equal(1, cache.Count());
        }

        </span><span style="background: white; color: blue">public </span><span style="background: white; color: #2b91af">TypeForTesting </span><span style="background: white; color: black">GetDataWithoutParameter()
        {
            </span><span style="background: white; color: blue">int </span><span style="background: white; color: black">expectedInt = 100;
            </span><span style="background: white; color: blue">return new </span><span style="background: white; color: #2b91af">TypeForTesting </span><span style="background: white; color: black">{ Id = expectedInt };
        }

        </span><span style="background: white; color: blue">public </span><span style="background: white; color: #2b91af">TypeForTesting </span><span style="background: white; color: black">GetDataWithParameter(</span><span style="background: white; color: blue">int </span><span style="background: white; color: black">arg1)
        {
            </span><span style="background: white; color: blue">int </span><span style="background: white; color: black">expectedInt = arg1;
            </span><span style="background: white; color: blue">return new </span><span style="background: white; color: #2b91af">TypeForTesting </span><span style="background: white; color: black">{ Id = expectedInt };
        }
    }

    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">TypeForTesting
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">public int </span><span style="background: white; color: black">Id { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
    }
}
</span></pre>
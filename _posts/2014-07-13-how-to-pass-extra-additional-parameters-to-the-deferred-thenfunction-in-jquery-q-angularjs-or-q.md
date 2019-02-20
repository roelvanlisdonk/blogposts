---
ID: 3952
post_title: >
  How to pass extra / additional
  parameters to the
  deferred.then()function in jQuery, $q
  (AngularJS) or Q.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/07/13/how-to-pass-extra-additional-parameters-to-the-deferred-thenfunction-in-jquery-q-angularjs-or-q/
published: true
post_date: 2014-07-13 20:00:06
---
<p>&#160;</p>  <h1>Q or $q</h1>  <p>If you are using Q or $q you can pas extra data to the then function by using the $q.all function:</p>  <pre class="code"><span style="background: white; color: blue">function </span><span style="background: white; color: black">execute()
{
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">firstNames = [</span><span style="background: white; color: #a31515">'Bo'</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">'Cris'</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">'Richard'</span><span style="background: white; color: black">];
    $q.all({
        firstNames: $q.when(firstNames),
        lastNames: $http.get(</span><span style="background: white; color: #a31515">'/api/lastNames'</span><span style="background: white; color: black">)
    }).then(handleGetLastNamesResult)
}

</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">handleGetLastNamesResult(data)
{
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">firstNames = data.firstNames;
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">lastNames = data.lastNames;
}</span></pre>


<p>&#160;</p>

<h1>jQuery</h1>

<p>&#160;</p>

<p>In this example I will use jQuery, but the same pattern works for $q and Q.</p>

<p>You can make an Ajax request in jQuery like, so:</p>

<pre class="code"><span style="background: white; color: blue">var </span><span style="background: white; color: black">app = (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
{
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">self = {};
        
    self.handleGetResult = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(data) {
        </span><span style="background: white; color: green">// Do something with the result from the server.
    </span><span style="background: white; color: black">};

    self.start = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
    {
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">promise = $.ajax({
            url: </span><span style="background: white; color: #a31515">'https://api.github.com/users/roelvanlisdonk/repos'</span><span style="background: white; color: black">,
            type: </span><span style="background: white; color: #a31515">'GET'
        </span><span style="background: white; color: black">});

        $.when(promise).then(self.handleGetResult);
    };

    self.start();

    </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">self;
})();</span></pre>

<p>The function passed to the .then function can only contain one parameter and will contain the data returned form the server. If you want to pass the function called by the “.then” function some additional data. You can use the following pattern:</p>

<p>&#160;</p>

<pre class="code"><span style="background: white; color: blue">var </span><span style="background: white; color: black">app = (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
{
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">self = {};
    
    self.handleGetResult = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(data) {
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">resultHandler = </span><span style="background: white; color: blue">this</span><span style="background: white; color: black">;
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">additionalData = resultHandler.getAdditionalData();

        </span><span style="background: white; color: green">// Do something with the result from the server and the additional data.
    </span><span style="background: white; color: black">};

    self.ResultHandler = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(additionalData, handleResultFunc) {
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">self = </span><span style="background: white; color: blue">this</span><span style="background: white; color: black">;
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">_additionalData = additionalData;
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">_handleResultFunc = handleResultFunc;

        self.getAdditionalData = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">_additionalData;
        };

        self.handleResult = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(data) {
            _handleResultFunc.call(self, data);
        };

        </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">self;
    };

    self.start = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
    {
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">promise = $.ajax({
            url: </span><span style="background: white; color: #a31515">'https://api.github.com/users/roelvanlisdonk/repos'</span><span style="background: white; color: black">,
            type: </span><span style="background: white; color: #a31515">'GET'
        </span><span style="background: white; color: black">});

        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">handler = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">self.ResultHandler(</span><span style="background: white; color: #a31515">&quot;Some extra data&quot;</span><span style="background: white; color: black">, self.handleGetResult);
        $.when(promise).then(handler.handleResult);
    };

    self.start();

    </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">self;
})();</span></pre>
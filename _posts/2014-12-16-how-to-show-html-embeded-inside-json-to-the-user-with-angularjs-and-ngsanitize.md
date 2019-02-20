---
ID: 4216
post_title: >
  How to show html embeded inside JSON to
  the user with AngularJS and ngSanitize.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/12/16/how-to-show-html-embeded-inside-json-to-the-user-with-angularjs-and-ngsanitize/
published: true
post_date: 2014-12-16 13:51:05
---
<p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/12/image9.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/12/image_thumb9.png" width="580" height="191" /></a></p>  <p>&#160;</p>  <p>I want to show HTML to the user, that was stored in a SQL Server Database. The data was queried from the SQL Server Database by using Entity Framework, then the C# model was converted to JSON, by using JSON.net and send to the browser by the ASP .NET web api service.</p>  <p>To show this HTML to the user with AngularJS, I used ngSanitize and the ng-bind-html directive:</p>  <p>(at this moment plunker is down, so I will edit this post in the future to add a plunker).</p>  <p>&#160;</p>  <p>If the HTML contains angular bindings / directives, you can use the compile service to bind the scope to the html fragment:</p>  <p><a title="https://docs.angularjs.org/api/ng/service/$compile" href="https://docs.angularjs.org/api/ng/service/$compile">https://docs.angularjs.org/api/ng/service/$compile</a></p>  <p>So instead of using the ng-bind-html, you can use this directive:</p>  <p><a title="https://github.com/incuna/angular-bind-html-compile/blob/master/angular-bind-html-compile.js" href="https://github.com/incuna/angular-bind-html-compile/blob/master/angular-bind-html-compile.js">https://github.com/incuna/angular-bind-html-compile/blob/master/angular-bind-html-compile.js</a></p>  <pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">!DOCTYPE </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">html </span><span style="background: white; color: red">xmlns:ng</span><span style="background: white; color: blue">=&quot;http://angularjs.org&quot; </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;ng-app&quot; </span><span style="background: white; color: red">ng-app</span><span style="background: white; color: blue">=&quot;spike&quot;&gt;
&lt;</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
    </span><span style="background: white; color: #006400">&lt;!-- Why is angular added to the html tag? Because IE8 won't work without it. --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">Spike page</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">charset</span><span style="background: white; color: blue">=&quot;utf-8&quot;&gt;
    </span><span style="background: white; color: #006400">&lt;!-- Why is &quot;edge&quot; used? Because we want the highest support for modern standards. --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">http-equiv</span><span style="background: white; color: blue">=&quot;X-UA-Compatible&quot; </span><span style="background: white; color: red">content</span><span style="background: white; color: blue">=&quot;IE=edge&quot;&gt;

    </span><span style="background: white; color: #006400">&lt;!-- Library scripts --&gt;
    &lt;!--&lt;script src=&quot;http://d3js.org/d3.v3.min.js&quot; charset=&quot;utf-8&quot;&gt;&lt;/script&gt;--&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;//ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;//ajax.googleapis.com/ajax/libs/angularjs/1.3.6/angular.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;//ajax.googleapis.com/ajax/libs/angularjs/1.3.6/angular-animate.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;//ajax.googleapis.com/ajax/libs/angularjs/1.3.6/angular-sanitize.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;

    </span><span style="background: white; color: #006400">&lt;!-- Live reload script with grunt. --&gt;
    &lt;!--&lt;script src=&quot;http://localhost:35729/livereload.js&quot;&gt;&lt;/script&gt;--&gt;

    &lt;!-- App styles --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;
        </span><span style="background: white; color: #006400">/*
            A small custom reset stylesheet is used, to fix style differences between browsers.
        */
        </span><span style="background: white; color: maroon">html</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">body
        </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">100%</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: maroon">body</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">div</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">p</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">ul</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">li</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">button
        </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">border</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">-webkit-box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">-moz-box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">font-family</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">&quot;Open Sans&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">sans-serif</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">margin</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">outline</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: maroon">body
        </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">background-color</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">#F1F1F1</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">20px</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: maroon">.spike-title
        </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">color</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">#393939</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: maroon">.spike-content
        </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">color</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">#393939</span><span style="background: white; color: black">;
        }
        </span><span style="background: white; color: maroon">.spike-content-with-class
        </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">color</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">#ff0000</span><span style="background: white; color: black">;
        }
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;

    </span><span style="background: white; color: #006400">&lt;!-- App scripts --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;

        </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
        {
            </span><span style="background: white; color: #a31515">&quot;use strict&quot;</span><span style="background: white; color: black">;

            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">app = angular.module(</span><span style="background: white; color: #a31515">&quot;spike&quot;</span><span style="background: white; color: black">, [</span><span style="background: white; color: #a31515">&quot;ngAnimate&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;ngSanitize&quot;</span><span style="background: white; color: black">]);
        }());

        (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
        {
            </span><span style="background: white; color: #a31515">&quot;use strict&quot;</span><span style="background: white; color: black">;

            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">app = angular.module(</span><span style="background: white; color: #a31515">&quot;spike&quot;</span><span style="background: white; color: black">);

            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">controller = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">($scope)
            {
                $scope.title = </span><span style="background: white; color: #a31515">&quot;How to show html embeded inside JSON to the user with AngularJS and ngSanitize.&quot;</span><span style="background: white; color: black">;

                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">json = </span><span style="background: white; color: #a31515">'{ \&quot;html\&quot;:\&quot;&lt;br&gt;&lt;br&gt;&lt;p&gt;Some html in JSON.&lt;/p&gt;&lt;br&gt;&lt;br&gt;&lt;p class=\\&quot;spike-content-with-class\\&quot;&gt;Some html in JSON with a class attribute.&lt;/p&gt;\&quot; }'</span><span style="background: white; color: black">;
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">content = JSON.parse(json);

                $scope.content = content.html;
            };

            app.controller(</span><span style="background: white; color: #a31515">&quot;main&quot;</span><span style="background: white; color: black">, [</span><span style="background: white; color: #a31515">&quot;$scope&quot;</span><span style="background: white; color: black">, controller]);
        }());
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">ng-controller</span><span style="background: white; color: blue">=&quot;main&quot;&gt;
        &lt;</span><span style="background: white; color: maroon">h2 </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;spike-title&quot;&gt;</span><span style="background: white; color: black">{{ </span><span style="background: white; color: purple">title </span><span style="background: white; color: black">}}</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">h2</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;spike-content&quot; </span><span style="background: white; color: red">ng-bind-html</span><span style="background: white; color: blue">=&quot;content&quot;&gt;&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
</span></pre>
---
ID: 4080
post_title: >
  How to sort items in a list with
  ng-repeat
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/10/27/how-to-sort-items-in-a-list-with-ng-repeat/
published: true
post_date: 2014-10-27 13:43:16
---
<p>Just a nice example on how to sort items in a list with ng-repeat:</p>  <p><a title="http://plnkr.co/edit/qa6LdhDdggApWPmOrwGD?p=preview" href="http://plnkr.co/edit/qa6LdhDdggApWPmOrwGD?p=preview">http://plnkr.co/edit/qa6LdhDdggApWPmOrwGD?p=preview</a></p>  <pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">!DOCTYPE </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">html </span><span style="background: white; color: red">xmlns:ng</span><span style="background: white; color: blue">=&quot;http://angularjs.org&quot; </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;ng-app&quot; </span><span style="background: white; color: red">ng-app</span><span style="background: white; color: blue">=&quot;spike&quot;&gt;
&lt;</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
    </span><span style="background: white; color: #006400">&lt;!--
        This page can be used as a base for spiking with jQuery, AngularJS and Kendo.
        All scripts and styles are loaded from a CDN or inline.
    --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">Spike page</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">charset</span><span style="background: white; color: blue">=&quot;utf-8&quot;&gt;
    &lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">http-equiv</span><span style="background: white; color: blue">=&quot;X-UA-Compatible&quot; </span><span style="background: white; color: red">content</span><span style="background: white; color: blue">=&quot;IE=edge&quot;&gt;</span><span style="background: white; color: #006400">&lt;!-- Use highest support for modern standards . --&gt;
    &lt;!-- Library styles --&gt;
</span><span style="background: white; color: blue">
    </span><span style="background: white; color: #006400">&lt;!-- Library scripts --&gt;
</span><span style="background: white; color: blue">    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;http://cdn.kendostatic.com/2014.2.1008/js/angular.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
</span><span style="background: white; color: blue">
    </span><span style="background: white; color: #006400">&lt;!-- App styles --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;
        </span><span style="background: white; color: #006400">/*
            A small custom reset stylesheet is used, to fix style differences between browsers.
        */
        </span><span style="background: white; color: maroon">html</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">body </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">100%</span><span style="background: white; color: black">; </span><span style="background: white; color: #006400">/* App layout uses a 100% height layout. */
        </span><span style="background: white; color: black">}

        </span><span style="background: white; color: maroon">body</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">div</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">p</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">ul</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">li </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">border</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">; </span><span style="background: white; color: #006400">/* Remove unwanted space. */
            </span><span style="background: white; color: red">-webkit-box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">; </span><span style="background: white; color: #006400">/* Place the border and padding inside the box. */
            </span><span style="background: white; color: red">-moz-box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">; </span><span style="background: white; color: #006400">/* Place the border and padding inside the box. */
            </span><span style="background: white; color: red">-ms-box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">; </span><span style="background: white; color: #006400">/* Place the border and padding inside the box. */
            </span><span style="background: white; color: red">-o-box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">; </span><span style="background: white; color: #006400">/* Place the border and padding inside the box. */
            </span><span style="background: white; color: red">box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">; </span><span style="background: white; color: #006400">/* Place the border and padding inside the box. */
            </span><span style="background: white; color: red">margin</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">; </span><span style="background: white; color: #006400">/* Remove unwanted space. */
            </span><span style="background: white; color: red">outline</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">; </span><span style="background: white; color: #006400">/* Remove unwanted space. */
            </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">; </span><span style="background: white; color: #006400">/* Remove unwanted space. */
        </span><span style="background: white; color: black">}

        </span><span style="background: white; color: maroon">body </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">20px</span><span style="background: white; color: black">; </span><span style="background: white; color: #006400">/* Create space between browser border and content. */
            </span><span style="background: white; color: red">min-width</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">320px</span><span style="background: white; color: black">; </span><span style="background: white; color: #006400">/* App will not work beneath width: 320px. */
        </span><span style="background: white; color: black">}

    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;

    </span><span style="background: white; color: #006400">&lt;!-- App scripts --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;

        </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
            </span><span style="background: white; color: #a31515">&quot;use strict&quot;</span><span style="background: white; color: black">;

            </span><span style="background: white; color: green">// This is the starting point (main) for the angular app.
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">app = angular.module(</span><span style="background: white; color: #a31515">&quot;spike&quot;</span><span style="background: white; color: black">, [</span><span style="background: white; color: #a31515">&quot;kendo.directives&quot;</span><span style="background: white; color: black">]);
        }());

        (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
            </span><span style="background: white; color: #a31515">&quot;use strict&quot;</span><span style="background: white; color: black">;

            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">app = angular.module(</span><span style="background: white; color: #a31515">&quot;spike&quot;</span><span style="background: white; color: black">);

            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">controller = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">($scope, service) {
                $scope.title = </span><span style="background: white; color: #a31515">&quot;Sort items in a list.&quot;</span><span style="background: white; color: black">;
                $scope.countriesAndCities = [
                    { </span><span style="background: white; color: #a31515">&quot;id&quot;</span><span style="background: white; color: black">: 1, </span><span style="background: white; color: #a31515">&quot;name&quot;</span><span style="background: white; color: black">: </span><span style="background: white; color: #a31515">&quot;The Netherlands&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;show&quot;</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">true</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;sort&quot;</span><span style="background: white; color: black">: 1 },
                    { </span><span style="background: white; color: #a31515">&quot;id&quot;</span><span style="background: white; color: black">: 2, </span><span style="background: white; color: #a31515">&quot;name&quot;</span><span style="background: white; color: black">: </span><span style="background: white; color: #a31515">&quot;Amsterdam&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;show&quot;</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">true</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;sort&quot;</span><span style="background: white; color: black">: 2 },
                    { </span><span style="background: white; color: #a31515">&quot;id&quot;</span><span style="background: white; color: black">: 3, </span><span style="background: white; color: #a31515">&quot;name&quot;</span><span style="background: white; color: black">: </span><span style="background: white; color: #a31515">&quot;Rotterdam&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;show&quot;</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">false</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;sort&quot;</span><span style="background: white; color: black">: 3 },
                    { </span><span style="background: white; color: #a31515">&quot;id&quot;</span><span style="background: white; color: black">: 4, </span><span style="background: white; color: #a31515">&quot;name&quot;</span><span style="background: white; color: black">: </span><span style="background: white; color: #a31515">&quot;US&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;show&quot;</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">false</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;sort&quot;</span><span style="background: white; color: black">: 4 },
                    { </span><span style="background: white; color: #a31515">&quot;id&quot;</span><span style="background: white; color: black">: 5, </span><span style="background: white; color: #a31515">&quot;name&quot;</span><span style="background: white; color: black">: </span><span style="background: white; color: #a31515">&quot;Las Vegas&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;show&quot;</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">true</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;sort&quot;</span><span style="background: white; color: black">: 5 },
                    { </span><span style="background: white; color: #a31515">&quot;id&quot;</span><span style="background: white; color: black">: 6, </span><span style="background: white; color: #a31515">&quot;name&quot;</span><span style="background: white; color: black">: </span><span style="background: white; color: #a31515">&quot;New York&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;show&quot;</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">true</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;sort&quot;</span><span style="background: white; color: black">: 6 }
                ];
            };

            app.controller(</span><span style="background: white; color: #a31515">&quot;main&quot;</span><span style="background: white; color: black">, [</span><span style="background: white; color: #a31515">&quot;$scope&quot;</span><span style="background: white; color: black">, controller]);
        }());
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">ng-controller</span><span style="background: white; color: blue">=&quot;main&quot;&gt;
        &lt;</span><span style="background: white; color: maroon">h2</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">{{ </span><span style="background: white; color: purple">title </span><span style="background: white; color: black">}}</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">h2</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">br </span><span style="background: white; color: blue">/&gt;
            </span><span style="background: white; color: black">Normal order:
            </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">br </span><span style="background: white; color: blue">/&gt;
            &lt;</span><span style="background: white; color: maroon">br </span><span style="background: white; color: blue">/&gt;
            &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">ng-repeat</span><span style="background: white; color: blue">=&quot;item in countriesAndCities | filter: { show: true } | orderBy:'sort':true&quot;&gt;
                </span><span style="background: white; color: black">{{ </span><span style="background: white; color: purple">item.name </span><span style="background: white; color: black">}}
            </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">br </span><span style="background: white; color: blue">/&gt;
            &lt;</span><span style="background: white; color: maroon">br </span><span style="background: white; color: blue">/&gt;
            </span><span style="background: white; color: black">Reversed order:
            </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">br </span><span style="background: white; color: blue">/&gt;
            &lt;</span><span style="background: white; color: maroon">br </span><span style="background: white; color: blue">/&gt;
            &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">ng-repeat</span><span style="background: white; color: blue">=&quot;item in countriesAndCities | filter: { show: true } | orderBy:'sort':false&quot;&gt;
                </span><span style="background: white; color: black">{{ </span><span style="background: white; color: purple">item.name </span><span style="background: white; color: black">}}
            </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
        &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;

</span></pre>
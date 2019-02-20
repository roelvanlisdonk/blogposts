---
ID: 4076
post_title: >
  Show hierarchy in combobox items, with
  Kendo and AngularJS.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/10/24/show-hierarchy-in-combobox-items-with-kendo-and-angularjs/
published: true
post_date: 2014-10-24 10:05:55
---
<p>Here is a plunkr showing a combobox with hierarchy:</p>  <p><a title="http://plnkr.co/edit/PaiRPD6dZNq0JaT2Tkdg?p=preview" href="http://plnkr.co/edit/PaiRPD6dZNq0JaT2Tkdg?p=preview">http://plnkr.co/edit/PaiRPD6dZNq0JaT2Tkdg?p=preview</a></p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/10/image4.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/10/image_thumb4.png" width="580" height="282" /></a></p>  <p>&#160;</p>  <pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">!DOCTYPE </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
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
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;http://cdn.kendostatic.com/2014.2.1008/styles/kendo.common.min.css&quot; </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;http://cdn.kendostatic.com/2014.2.1008/styles/kendo.silver.min.css&quot; </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;http://cdn.kendostatic.com/2014.2.1008/styles/kendo.silver.mobile.min.css&quot; </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;http://cdn.kendostatic.com/2014.2.1008/styles/kendo.dataviz.min.css&quot; </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;http://cdn.kendostatic.com/2014.2.1008/styles/kendo.dataviz.silver.min.css&quot; </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; /&gt;

    </span><span style="background: white; color: #006400">&lt;!-- Library scripts --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;http://cdn.kendostatic.com/2014.2.1008/js/jquery.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;http://cdn.kendostatic.com/2014.2.1008/js/angular.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;http://cdn.kendostatic.com/2014.2.1008/js/kendo.all.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;

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

        </span><span style="background: white; color: maroon">.level1 </span><span style="background: white; color: black">{

        }
        </span><span style="background: white; color: maroon">.level2 </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">padding-left</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">30px</span><span style="background: white; color: black">;
        }
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
                $scope.title = </span><span style="background: white; color: #a31515">&quot;Show hierarchy in combobox items, with Kendo and AngularJS.&quot;</span><span style="background: white; color: black">;
                $scope.countriesAndCities = [
                    { </span><span style="background: white; color: #a31515">&quot;id&quot;</span><span style="background: white; color: black">: 1, </span><span style="background: white; color: #a31515">&quot;name&quot;</span><span style="background: white; color: black">: </span><span style="background: white; color: #a31515">&quot;The Netherlands&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;level&quot;</span><span style="background: white; color: black">: 1 },
                    { </span><span style="background: white; color: #a31515">&quot;id&quot;</span><span style="background: white; color: black">: 2, </span><span style="background: white; color: #a31515">&quot;name&quot;</span><span style="background: white; color: black">: </span><span style="background: white; color: #a31515">&quot;Amsterdam&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;level&quot;</span><span style="background: white; color: black">: 2 },
                    { </span><span style="background: white; color: #a31515">&quot;id&quot;</span><span style="background: white; color: black">: 3, </span><span style="background: white; color: #a31515">&quot;name&quot;</span><span style="background: white; color: black">: </span><span style="background: white; color: #a31515">&quot;Rotterdam&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;level&quot;</span><span style="background: white; color: black">: 2 },
                    { </span><span style="background: white; color: #a31515">&quot;id&quot;</span><span style="background: white; color: black">: 4, </span><span style="background: white; color: #a31515">&quot;name&quot;</span><span style="background: white; color: black">: </span><span style="background: white; color: #a31515">&quot;US&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;level&quot;</span><span style="background: white; color: black">: 1 },
                    { </span><span style="background: white; color: #a31515">&quot;id&quot;</span><span style="background: white; color: black">: 5, </span><span style="background: white; color: #a31515">&quot;name&quot;</span><span style="background: white; color: black">: </span><span style="background: white; color: #a31515">&quot;Las Vegas&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;level&quot;</span><span style="background: white; color: black">: 2 },
                    { </span><span style="background: white; color: #a31515">&quot;id&quot;</span><span style="background: white; color: black">: 6, </span><span style="background: white; color: #a31515">&quot;name&quot;</span><span style="background: white; color: black">: </span><span style="background: white; color: #a31515">&quot;New York&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;level&quot;</span><span style="background: white; color: black">: 2 }
                ];

                $scope.customTemplate = $(</span><span style="background: white; color: #a31515">&quot;#customTemplate&quot;</span><span style="background: white; color: black">).html();
            };

            app.controller(</span><span style="background: white; color: #a31515">&quot;main&quot;</span><span style="background: white; color: black">, [</span><span style="background: white; color: #a31515">&quot;$scope&quot;</span><span style="background: white; color: black">, controller]);
        }());
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">ng-controller</span><span style="background: white; color: blue">=&quot;main&quot;&gt;
        &lt;</span><span style="background: white; color: maroon">h2</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">{{ </span><span style="background: white; color: purple">title </span><span style="background: white; color: black">}}</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">h2</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">select </span><span style="background: white; color: red">kendo-combo-box
                    k-template</span><span style="background: white; color: blue">=&quot;customTemplate&quot;
                    </span><span style="background: white; color: red">k-placeholder</span><span style="background: white; color: blue">=&quot;'Choose country'&quot;
                    </span><span style="background: white; color: red">k-filter</span><span style="background: white; color: blue">=&quot;contains&quot;
                    </span><span style="background: white; color: red">k-data-source</span><span style="background: white; color: blue">=&quot;countriesAndCities&quot;
                    </span><span style="background: white; color: red">data-text-field</span><span style="background: white; color: blue">=&quot;'name'&quot;
                    </span><span style="background: white; color: red">data-value-field</span><span style="background: white; color: blue">=&quot;'id'&quot;
                    </span><span style="background: white; color: red">k-auto-bind</span><span style="background: white; color: blue">=&quot;false&quot;&gt;&lt;/</span><span style="background: white; color: maroon">select</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;customTemplate&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/x-kendo-template&quot;&gt;
                &lt;</span><span style="background: white; color: maroon">span </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;k-state-default level#= level #&quot;&gt;
                    </span><span style="background: white; color: black">#= name #
                </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">span</span><span style="background: white; color: blue">&gt;
            &lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
        &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;

</span></pre>
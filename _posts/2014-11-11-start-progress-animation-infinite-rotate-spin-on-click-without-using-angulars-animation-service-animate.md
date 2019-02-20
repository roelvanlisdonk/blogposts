---
ID: 4125
post_title: >
  Start progress animation (infinite
  rotate / spin) on click, without using
  angulars animation service ($animate).
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/11/11/start-progress-animation-infinite-rotate-spin-on-click-without-using-angulars-animation-service-animate/
published: true
post_date: 2014-11-11 15:20:12
---
<p>&#160;</p>  <p>See code at, Plunker: <a title="http://plnkr.co/edit/jUzCC1FmtgxdX4gWTVIW?p=preview" href="http://plnkr.co/edit/jUzCC1FmtgxdX4gWTVIW?p=preview">http://plnkr.co/edit/jUzCC1FmtgxdX4gWTVIW?p=preview</a></p>  <p>&#160;</p>  <p>I used a custom directive with isolated scope:</p>  <pre class="code"><span style="background: white; color: #006400">&lt;!-- App scripts --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;

        </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
            </span><span style="background: white; color: #a31515">&quot;use strict&quot;</span><span style="background: white; color: black">;

            </span><span style="background: white; color: green">// This is the starting point (main) for the angular app.
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">app = angular.module(</span><span style="background: white; color: #a31515">&quot;spike&quot;</span><span style="background: white; color: black">, [</span><span style="background: white; color: black">]);

</span><span style="background: white; color: black">
        }());
   
        (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
            </span><span style="background: white; color: #a31515">&quot;use strict&quot;</span><span style="background: white; color: black">;

            </span><span style="background: white; color: green">// Adds an animation to an element.
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">directive = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
                </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">link($scope, element, attributes, controller) {

                    $scope.$watch(</span><span style="background: white; color: #a31515">'loading'</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(newValue, oldValue) {
                        </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(newValue === </span><span style="background: white; color: blue">true</span><span style="background: white; color: black">) {
                            element.removeClass(</span><span style="background: white; color: #a31515">&quot;progress-indicator fa fa-refresh spin&quot;</span><span style="background: white; color: black">);
                            element.addClass(</span><span style="background: white; color: #a31515">&quot;progress-indicator fa fa-refresh spin&quot;</span><span style="background: white; color: black">);
                        }
                        </span><span style="background: white; color: blue">else </span><span style="background: white; color: black">{
                            element.removeClass(</span><span style="background: white; color: #a31515">&quot;progress-indicator fa fa-refresh spin&quot;</span><span style="background: white; color: black">);
                        }
                    });   
                }

                </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">{
                    restrict: </span><span style="background: white; color: #a31515">&quot;EA&quot;</span><span style="background: white; color: black">,  </span><span style="background: white; color: green">// Directive be used as element and as attribute.
                    </span><span style="background: white; color: black">link: link,
                    scope: {
                        </span><span style="background: white; color: green">// This directive expects an attribute &quot;loading&quot;.
                        // The value of the attribute &quot;loading&quot; will be watched.
                        // When this value === true, classes will be added to &quot;show&quot; and animate a progressindicator.
                        // When this value !== true, classes will be removed, to stop animation and &quot;hide&quot; the progressindicator.
                        </span><span style="background: white; color: black">loading: </span><span style="background: white; color: #a31515">&quot;=loading&quot;
                    </span><span style="background: white; color: black">}
                };
            };

            angular.module(</span><span style="background: white; color: #a31515">'spike'</span><span style="background: white; color: black">).directive(</span><span style="background: white; color: #a31515">'zvdzProgress'</span><span style="background: white; color: black">, [directive]);
        }());

        (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
            </span><span style="background: white; color: #a31515">&quot;use strict&quot;</span><span style="background: white; color: black">;

            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">app = angular.module(</span><span style="background: white; color: #a31515">&quot;spike&quot;</span><span style="background: white; color: black">);

            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">controller = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">($scope, $animate) {
                $scope.title = </span><span style="background: white; color: #a31515">&quot;Start progress animation on click.&quot;</span><span style="background: white; color: black">;
               
                $scope.isLoading = </span><span style="background: white; color: blue">false</span><span style="background: white; color: black">;

                $scope.start = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
                    $scope.isLoading = </span><span style="background: white; color: blue">true</span><span style="background: white; color: black">;
                };

                $scope.stop = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
                    $scope.isLoading = </span><span style="background: white; color: blue">false</span><span style="background: white; color: black">;
                };
            };

            app.controller(</span><span style="background: white; color: #a31515">&quot;main&quot;</span><span style="background: white; color: black">, [</span><span style="background: white; color: #a31515">&quot;$scope&quot;</span><span style="background: white; color: black">, controller]);
        }());
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;</span></pre>


<p>&#160;</p>

<pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">ng-controller</span><span style="background: white; color: blue">=&quot;main&quot;&gt;
        &lt;</span><span style="background: white; color: maroon">h2</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">{{ </span><span style="background: white; color: purple">title </span><span style="background: white; color: black">}}</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">h2</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">br </span><span style="background: white; color: blue">/&gt;
            &lt;</span><span style="background: white; color: maroon">button </span><span style="background: white; color: red">ng-click</span><span style="background: white; color: blue">=&quot;start()&quot;&gt;</span><span style="background: white; color: black">Start</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">button</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">br </span><span style="background: white; color: blue">/&gt;
            &lt;</span><span style="background: white; color: maroon">br </span><span style="background: white; color: blue">/&gt;
            &lt;</span><span style="background: white; color: maroon">button </span><span style="background: white; color: red">ng-click</span><span style="background: white; color: blue">=&quot;stop()&quot;&gt;</span><span style="background: white; color: black">Stop</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">button</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">br </span><span style="background: white; color: blue">/&gt;
            &lt;</span><span style="background: white; color: maroon">br </span><span style="background: white; color: blue">/&gt;
            &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">zvdz-progress loading</span><span style="background: white; color: blue">=&quot;isLoading&quot;&gt;&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
        &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;</span></pre>


<p>&#160;</p>

<p>&#160;</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/11/image.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/11/image_thumb.png" width="580" height="102" /></a></p>

<p>&#160;</p>

<p>On start ng-click, a refresh icon is shown that spins:</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/11/image1.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/11/image_thumb1.png" width="580" height="117" /></a></p>
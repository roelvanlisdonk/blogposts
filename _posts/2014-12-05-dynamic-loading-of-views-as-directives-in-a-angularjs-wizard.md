---
ID: 4196
post_title: >
  Dynamic loading of views as directives
  in an AngularJS wizard.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/12/05/dynamic-loading-of-views-as-directives-in-a-angularjs-wizard/
published: true
post_date: 2014-12-05 16:01:56
---
<p>Demo and Code can be found at: <a title="http://plnkr.co/edit/Ht4ud6kyJUzDTQdS9MI2?p=preview" href="http://plnkr.co/edit/Ht4ud6kyJUzDTQdS9MI2?p=preview">http://plnkr.co/edit/Ht4ud6kyJUzDTQdS9MI2?p=preview</a></p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/12/image5.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/12/image_thumb5.png" width="580" height="258" /></a></p>  <p>&#160;</p>  <p>Just for the fun, I added a D3.js chart:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/12/image6.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/12/image_thumb6.png" width="576" height="333" /></a></p>  <p>&#160;</p>  <p>A simple AngularJS wizard that dynamically loads pages (views). </p>  <p>In the plunker each page is a *.html file that is loaded by dynamically setting a viewmodel property “pageTemplateUrl”:</p>  <pre class="code"><span style="background: white; color: red">ng-include</span><span style="background: white; color: blue">=&quot;pageTemplateUrl&quot;</span></pre>


<p>Each *.html file contains a “page” directive.</p>

<p>In this examples all pages share one “page” directive, so all logic for all pages is stored in the “page” directive, but you can put in, any custom made directive in the “*.html” file, so you can give each page it’s own directive / logic.</p>

<p>&#160;</p>

<p><strong>Index.html</strong></p>

<pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">ng-controller</span><span style="background: white; color: blue">=&quot;main&quot;&gt;
        &lt;</span><span style="background: white; color: maroon">h2 </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;main-title&quot;&gt;</span><span style="background: white; color: black">{{ </span><span style="background: white; color: purple">title </span><span style="background: white; color: black">}}</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">h2</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">wizard</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: maroon">wizard</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;</span></pre>


<p><strong>Wizard.html</strong></p>

<pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;wizard&quot;&gt;
    &lt;</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">Wizard</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;page page-slide-in&quot; </span><span style="background: white; color: red">ng-include</span><span style="background: white; color: blue">=&quot;pageTemplateUrl&quot;&gt;&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;footer flex-horizontal&quot;&gt;
        &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;wizard-footer-left&quot;&gt;
            &lt;</span><span style="background: white; color: maroon">button </span><span style="background: white; color: red">ng-disabled</span><span style="background: white; color: blue">=&quot;prevShouldBeDisabled()&quot;
                    </span><span style="background: white; color: red">ng-click</span><span style="background: white; color: blue">=&quot;prev()&quot;&gt;
                </span><span style="background: white; color: black">Back
            </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">button</span><span style="background: white; color: blue">&gt;
        &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;wizard-footer-middle flex-vertical&quot;&gt;
            &lt;</span><span style="background: white; color: maroon">ul </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;steps&quot;&gt;
                &lt;</span><span style="background: white; color: maroon">li </span><span style="background: white; color: red">ng-repeat</span><span style="background: white; color: blue">=&quot;page in pages&quot;
                    </span><span style="background: white; color: red">ng-class</span><span style="background: white; color: blue">=&quot;{ active: isActive(page), complete: isCompleted(page) }&quot;
                    </span><span style="background: white; color: red">ng-click</span><span style="background: white; color: blue">=&quot;setPageTemplateUrl(page)&quot;&gt;
                    &lt;</span><span style="background: white; color: maroon">span </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;badge&quot;&gt;</span><span style="background: white; color: black">{{ </span><span style="background: white; color: purple">$index + 1 </span><span style="background: white; color: black">}}</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">span</span><span style="background: white; color: blue">&gt;
                    </span><span style="background: white; color: black">{{ </span><span style="background: white; color: purple">page.title </span><span style="background: white; color: black">}}
                    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">span </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;chevron&quot;&gt;&lt;/</span><span style="background: white; color: maroon">span</span><span style="background: white; color: blue">&gt;
                &lt;/</span><span style="background: white; color: maroon">li</span><span style="background: white; color: blue">&gt;

            &lt;/</span><span style="background: white; color: maroon">ul</span><span style="background: white; color: blue">&gt;
        &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;wizard-footer-right&quot;&gt;
            &lt;</span><span style="background: white; color: maroon">button </span><span style="background: white; color: red">ng-disabled</span><span style="background: white; color: blue">=&quot;nextShouldBeDisabled()&quot;
                    </span><span style="background: white; color: red">ng-click</span><span style="background: white; color: blue">=&quot;next()&quot;&gt;
                </span><span style="background: white; color: black">Next
            </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">button</span><span style="background: white; color: blue">&gt;
        &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
</span></pre>


<p><strong>Intro.html (first page in wizard)</strong></p>

<pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">page</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;page-title&quot;&gt;</span><span style="background: white; color: black">{{ </span><span style="background: white; color: purple">title </span><span style="background: white; color: black">}}</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">p</span><span style="background: white; color: blue">&gt;
        </span><span style="background: white; color: black">Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. <br />        Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. <br />        Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. Nulla consequat massa quis enim.<br />        Donec pede justo, fringilla vel, aliquet nec, vulputate eget, arcu. <br />        In enim justo, rhoncus ut, imperdiet a, venenatis vitae, justo. <br />        Nullam dictum felis eu pede mollis pretium. Integer tincidunt. Cras dapibus. <br />        Vivamus elementum semper nisi. Aenean vulputate eleifend tellus. Aenean leo ligula, porttitor eu, <br />        consequat vitae, eleifend ac, enim. Aliquam lorem ante, dapibus in, viverra quis, feugiat a, tellus. <br />        Phasellus viverra nulla ut metus varius laoreet. Quisque rutrum. Aenean imperdiet. <br />        Etiam ultricies nisi vel augue. Curabitur ullamcorper ultricies nisi. Nam eget dui.
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">p</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">page</span><span style="background: white; color: blue">&gt;
</span></pre>


<p><strong>JavaScript</strong></p>


<pre class="code"><span style="background: white; color: black">        (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
        {
            </span><span style="background: white; color: #a31515">&quot;use strict&quot;</span><span style="background: white; color: black">;

            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">app = angular.module(</span><span style="background: white; color: #a31515">&quot;spike&quot;</span><span style="background: white; color: black">, [</span><span style="background: white; color: #a31515">&quot;ngAnimate&quot;</span><span style="background: white; color: black">]);
        }());

        (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
        {
            </span><span style="background: white; color: #a31515">&quot;use strict&quot;</span><span style="background: white; color: black">;

            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">app = angular.module(</span><span style="background: white; color: #a31515">&quot;spike&quot;</span><span style="background: white; color: black">);

            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">controller = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">($scope)
            {
                console.log(</span><span style="background: white; color: #a31515">&quot;Controller [main] loaded.&quot;</span><span style="background: white; color: black">);
                $scope.title = </span><span style="background: white; color: #a31515">&quot;Dynamic loading of views as directives in a AngularJS wizard.&quot;</span><span style="background: white; color: black">;
            };

            app.controller(</span><span style="background: white; color: #a31515">&quot;main&quot;</span><span style="background: white; color: black">, [</span><span style="background: white; color: #a31515">&quot;$scope&quot;</span><span style="background: white; color: black">, controller]);
        }());

        (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
        {
            </span><span style="background: white; color: #a31515">&quot;use strict&quot;</span><span style="background: white; color: black">;

            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">directive = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
            {
                </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">link($scope, element, attributes, controller)
                {
                    </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">initialize()
                    {
                        showPage(0);
                    }

                    </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">showPage(pageId)
                    {
                        $scope.selectedPageId = pageId;
                        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">page = $scope.pages[$scope.selectedPageId];
                        $scope.setPageTemplateUrl(page);
                    }

                    $scope.chartData = [10, 20, 30, 40, 60, 80, 20, 50];

                    $scope.pages = [
                        { 
                            title: </span><span style="background: white; color: #a31515">&quot;intro&quot;
                        </span><span style="background: white; color: black">},
                        {
                            title: </span><span style="background: white; color: #a31515">&quot;modules&quot;
                        </span><span style="background: white; color: black">},
                        {
                            title: </span><span style="background: white; color: #a31515">&quot;detail&quot;
                        </span><span style="background: white; color: black">},
                        {
                            title: </span><span style="background: white; color: #a31515">&quot;order&quot;
                        </span><span style="background: white; color: black">}
                    ];

                    $scope.isActive = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(page)
                    {
                        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">selectedPage = $scope.pages[$scope.selectedPageId];
                        </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">(selectedPage.title === page.title);
                    };

                    $scope.isCompleted = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(page)
                    {
                        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">index = $scope.pages.indexOf(page);
                        </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">(index &lt; $scope.selectedPageId);
                    };

                    $scope.next = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
                    {
                        showPage($scope.selectedPageId + 1);
                    };

                    $scope.prev = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
                    {
                        showPage($scope.selectedPageId - 1);
                    };

                    $scope.nextShouldBeDisabled = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
                    {
                        </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">($scope.selectedPageId &gt;= $scope.pages.length - 1);
                    };

                    $scope.prevShouldBeDisabled = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
                    {
                        </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">($scope.selectedPageId &lt;= 0);
                    };

                    $scope.setPageTemplateUrl = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(page)
                    {
                        $scope.selectedPageId = $scope.pages.indexOf(page);
                        $scope.pageTemplateUrl = page.title + </span><span style="background: white; color: #a31515">&quot;.html&quot;</span><span style="background: white; color: black">;
                    };

                    initialize();

                    console.log(</span><span style="background: white; color: #a31515">&quot;Directive [wizard] loaded.&quot;</span><span style="background: white; color: black">);
                }

                </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">{
                    restrict: </span><span style="background: white; color: #a31515">&quot;EA&quot;</span><span style="background: white; color: black">,
                    link: link,
                    templateUrl: </span><span style="background: white; color: #a31515">&quot;wizard.html&quot;
                </span><span style="background: white; color: black">};
            };

            angular.module(</span><span style="background: white; color: #a31515">&quot;spike&quot;</span><span style="background: white; color: black">).directive(</span><span style="background: white; color: #a31515">&quot;wizard&quot;</span><span style="background: white; color: black">, [directive]);
        }());

        (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
        {
            </span><span style="background: white; color: #a31515">&quot;use strict&quot;</span><span style="background: white; color: black">;

            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">directive = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
            {
                </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">link($scope, element, attributes, controller)
                {
                    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">page = $scope.pages[$scope.selectedPageId];
                    $scope.title = page.title;

                    

                    console.log(</span><span style="background: white; color: #a31515">&quot;Directive [page].[&quot; </span><span style="background: white; color: black">+ page.title + </span><span style="background: white; color: #a31515">&quot;] loaded.&quot;</span><span style="background: white; color: black">);
                }

                </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">{
                    restrict: </span><span style="background: white; color: #a31515">&quot;EA&quot;</span><span style="background: white; color: black">,
                    link: link
                };
            };

            angular.module(</span><span style="background: white; color: #a31515">&quot;spike&quot;</span><span style="background: white; color: black">).directive(</span><span style="background: white; color: #a31515">&quot;page&quot;</span><span style="background: white; color: black">, [directive]);
        }());

        (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
        {
            </span><span style="background: white; color: #a31515">&quot;use strict&quot;</span><span style="background: white; color: black">;

            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">directive = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
            {
                </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">link($scope, element, attributes, controller)
                {
                    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">chart = d3.select(element[0]);
                    chart.append(</span><span style="background: white; color: #a31515">&quot;div&quot;</span><span style="background: white; color: black">).attr(</span><span style="background: white; color: #a31515">&quot;class&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">&quot;chart&quot;</span><span style="background: white; color: black">)
                     .selectAll(</span><span style="background: white; color: #a31515">'div'</span><span style="background: white; color: black">)
                     .data($scope.data).enter().append(</span><span style="background: white; color: #a31515">&quot;div&quot;</span><span style="background: white; color: black">)
                     .transition().ease(</span><span style="background: white; color: #a31515">&quot;elastic&quot;</span><span style="background: white; color: black">)
                     .style(</span><span style="background: white; color: #a31515">&quot;width&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(d) { </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">d + </span><span style="background: white; color: #a31515">&quot;%&quot;</span><span style="background: white; color: black">; })
                     .text(</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(d) { </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">d + </span><span style="background: white; color: #a31515">&quot;%&quot;</span><span style="background: white; color: black">; });

                    console.log(</span><span style="background: white; color: #a31515">&quot;Directive [barsChart] loaded.&quot;</span><span style="background: white; color: black">);
                }

                </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">{
                    restrict: </span><span style="background: white; color: #a31515">&quot;EA&quot;</span><span style="background: white; color: black">,
                    replace: </span><span style="background: white; color: blue">false</span><span style="background: white; color: black">,
                    scope: {data: </span><span style="background: white; color: #a31515">'=chartData'</span><span style="background: white; color: black">},
                    link: link
                };
            };

            angular.module(</span><span style="background: white; color: #a31515">&quot;spike&quot;</span><span style="background: white; color: black">).directive(</span><span style="background: white; color: #a31515">&quot;barsChart&quot;</span><span style="background: white; color: black">, [directive]);
        }());</span></pre>
---
ID: 3797
post_title: >
  Dynamically change kendo ui grid columns
  with AngularJS
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/05/27/dynamically-change-kendo-ui-grid-columns-with-angularjs/
published: true
post_date: 2014-05-27 17:07:00
---
<p>The following HTML / JavaScript explains how to dynamically change Kendo UI grid columns, by using the Kendo – Angular directives.</p>  <p>&#160;</p>  <pre class="code"><p><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">!doctype </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">html </span><span style="background: white; color: red">ng-app</span><span style="background: white; color: blue">=&quot;researchApp&quot;&gt;
&lt;</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">charset</span><span style="background: white; color: blue">=&quot;utf-8&quot;&gt;
&lt;</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">Dynamically change Kendo grid columns.</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;/Client/Libraries/Kendo/css/kendo.common.min.css&quot; </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot; /&gt;
&lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;/Client/Libraries/Kendo/css/kendo.silver.min.css&quot; </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot; /&gt;
&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;/Client/Libraries/Kendo/js/jquery.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;/Client/Libraries/Angular/angular.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;/Client/Libraries/Angular/angular-route.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;/Client/Libraries/Angular/angular-sanitize.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;/Client/Libraries/Kendo/js/kendo.all.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;/Client/Libraries/Angular/angular-kendo.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;/Client/Libraries/Q/q.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;/Client/Libraries/Breeze/breeze.debug.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body </span><span style="background: white; color: red">ng-controller</span><span style="background: white; color: blue">=&quot;researchCtrl&quot;&gt;
&lt;</span><span style="background: white; color: maroon">button </span><span style="background: white; color: red">ng-click</span><span style="background: white; color: blue">=&quot;execute1($event)&quot;&gt;</span><span style="background: white; color: black">Execute 1</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">button</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">button </span><span style="background: white; color: red">ng-click</span><span style="background: white; color: blue">=&quot;execute2($event)&quot;&gt;</span><span style="background: white; color: black">Execute 2</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">button</span><span style="background: white; color: blue">&gt;
</span><span style="background: white; color: #006400">&lt;!-- By supplying the string &quot;grid&quot; to the kendo-grid directive, the kendo grid will be made available</span></p><p><span style="background: white; color: #006400"> to the $scope as $scope.grid. --&gt;
&lt;!-- All initial configuration of the kendo grid is provided by the $scope.gridOptions. --&gt;
&lt;!-- The kendo grid will &quot;refresh&quot; / &quot;rebind&quot; itself, when the $scope.selectedType changes. --&gt;
</span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">kendo-grid</span><span style="background: white; color: blue">=&quot;grid&quot; </span><span style="background: white; color: red">k-options</span><span style="background: white; color: blue">=&quot;gridOptions&quot; </span><span style="background: white; color: red">k-rebind</span><span style="background: white; color: blue">=&quot;selectedType&quot;&gt;&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
</span><span style="background: white; color: green">// Main entry point of the application.
// Kendo - Angular needs the [&quot;kendo.directives&quot;] to be injected.
</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">researchApp = angular.module(</span><span style="background: white; color: #a31515">&quot;researchApp&quot;</span><span style="background: white; color: black">, [</span><span style="background: white; color: #a31515">&quot;kendo.directives&quot;</span><span style="background: white; color: black">]);
researchApp.controller(</span><span style="background: white; color: #a31515">'researchCtrl'</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">($scope)
{
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">GridModel1 = kendo.data.Model.define({
        id: </span><span style="background: white; color: #a31515">'Id'</span><span style="background: white; color: black">,
        fields: {
            company: { type: </span><span style="background: white; color: #a31515">'string' </span><span style="background: white; color: black">},
            os: { type: </span><span style="background: white; color: #a31515">'string' </span><span style="background: white; color: black">}
        }
    });

    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">GridModel2 = kendo.data.Model.define({
        id: </span><span style="background: white; color: #a31515">'Id'</span><span style="background: white; color: black">,
        fields: {
            FirstName: { type: </span><span style="background: white; color: #a31515">'string' </span><span style="background: white; color: black">},
            LastName: { type: </span><span style="background: white; color: #a31515">'string' </span><span style="background: white; color: black">},
            Description: { type: </span><span style="background: white; color: #a31515">'string' </span><span style="background: white; color: black">}
        }
    });

    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">gridOptions1 = {
        dataSource: </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">kendo.data.DataSource({
            data: </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">kendo.data.ObservableArray([
                </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">GridModel1({
                    Id: 1,
                    company: </span><span style="background: white; color: #a31515">'Apple'</span><span style="background: white; color: black">,
                    os: </span><span style="background: white; color: #a31515">'OSX'
                </span><span style="background: white; color: black">})
            ]),
            schema: {
                model: GridModel1
            }
        })
    };

    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">gridOptions2 = {
        dataSource: </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">kendo.data.DataSource({
            data: </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">kendo.data.ObservableArray([
                </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">GridModel2({
                    Id: 1, FirstName: </span><span style="background: white; color: #a31515">'John'</span><span style="background: white; color: black">,
                    LastName: </span><span style="background: white; color: #a31515">'Do'</span><span style="background: white; color: black">,
                    Description: </span><span style="background: white; color: #a31515">&quot;My test description.&quot;
                </span><span style="background: white; color: black">})
            ]),
            schema: {
                model: GridModel2
            }
        })
    };

    </span><span style="background: white; color: green">// Selected type is used to rebind the kendo ui grid.
    </span><span style="background: white; color: black">$scope.selectedType = </span><span style="background: white; color: #a31515">&quot;&quot;</span><span style="background: white; color: black">;
    $scope.gridOptions = gridOptions1;
    $scope.execute1 = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(e)
    {
        </span><span style="background: white; color: green">// Switch 
        </span><span style="background: white; color: black">$scope.gridOptions = gridOptions1;
        $scope.selectedType = </span><span style="background: white; color: #a31515">&quot;Software&quot;</span><span style="background: white; color: black">;
    };
    $scope.execute2 = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(e)
    {
        $scope.gridOptions = gridOptions2;
        $scope.selectedType = </span><span style="background: white; color: #a31515">&quot;Employee&quot;</span><span style="background: white; color: black">;
    };
});
</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;</span></p></pre>


<p>Initial screendump:</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/05/image8.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/05/image_thumb8.png" width="580" height="117" /></a></p>

<p>&#160;</p>

<p>Screendump after clicking on the “Execute 2” button:</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/05/image9.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/05/image_thumb9.png" width="580" height="136" /></a></p>
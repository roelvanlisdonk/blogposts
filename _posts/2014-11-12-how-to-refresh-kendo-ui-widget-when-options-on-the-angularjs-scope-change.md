---
ID: 4133
post_title: >
  How to refresh a kendo ui widget, when
  options on the AngularJS $scope change.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/11/12/how-to-refresh-kendo-ui-widget-when-options-on-the-angularjs-scope-change/
published: true
post_date: 2014-11-12 14:46:51
---
Code can be found at: <a title="http://plnkr.co/edit/8CQURTLHftIpBwXUAN7s?p=preview" href="http://plnkr.co/edit/8CQURTLHftIpBwXUAN7s?p=preview">http://plnkr.co/edit/8CQURTLHftIpBwXUAN7s?p=preview</a>

&nbsp;

Let say, we want to show <strong>all</strong> records in a pageable kendo-grid, when the user clicks on a button.

This can accomplished by programmatically setting the page size of a kendo-grid and using the k-rebind attribute:

&nbsp;

<a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/11/image2.png" rel="lightbox"><img style="background-image: none; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border: 0px;" title="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/11/image_thumb2.png" alt="image" width="482" height="323" border="0" /></a>

&nbsp;

After clicking on the “Set page size” button:

&nbsp;

<a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/11/image3.png" rel="lightbox"><img style="background-image: none; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border: 0px;" title="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/11/image_thumb3.png" alt="image" width="580" height="460" border="0" /></a>

&nbsp;
<pre class="code"><span style="background: white; color: #006400;">&lt;!-- App scripts --&gt;
    </span><span style="background: white; color: blue;">&lt;</span><span style="background: white; color: maroon;">script</span><span style="background: white; color: blue;">&gt;

        </span><span style="background: white; color: black;">(</span><span style="background: white; color: blue;">function </span><span style="background: white; color: black;">() {
            </span><span style="background: white; color: #a31515;">"use strict"</span><span style="background: white; color: black;">;

            </span><span style="background: white; color: green;">// This is the starting point (main) for the angular app.
            </span><span style="background: white; color: blue;">var </span><span style="background: white; color: black;">app = angular.module(</span><span style="background: white; color: #a31515;">"spike"</span><span style="background: white; color: black;">, [</span><span style="background: white; color: #a31515;">"kendo.directives"</span><span style="background: white; color: black;">]);

            </span><span style="background: white; color: green;">// Set culture info to Ducth:
            </span><span style="background: white; color: black;">kendo.culture(</span><span style="background: white; color: #a31515;">"nl-NL"</span><span style="background: white; color: black;">);
        }());
   
        </span><span style="background: white; color: black;">
        (</span><span style="background: white; color: blue;">function </span><span style="background: white; color: black;">() {
            </span><span style="background: white; color: #a31515;">"use strict"</span><span style="background: white; color: black;">;

            </span><span style="background: white; color: blue;">var </span><span style="background: white; color: black;">app = angular.module(</span><span style="background: white; color: #a31515;">"spike"</span><span style="background: white; color: black;">);

            </span><span style="background: white; color: blue;">var </span><span style="background: white; color: black;">controller = </span><span style="background: white; color: blue;">function </span><span style="background: white; color: black;">($scope, $animate) {
                $scope.title = </span><span style="background: white; color: #a31515;">"Programmatically set pagesize kendo grid."</span><span style="background: white; color: black;">;
                
                </span><span style="background: white; color: blue;">var </span><span style="background: white; color: black;">data = [
                    { id: 1, name: </span><span style="background: white; color: #a31515;">"Bob1" </span><span style="background: white; color: black;">},
                    { id: 2, name: </span><span style="background: white; color: #a31515;">"Bob2" </span><span style="background: white; color: black;">},
                    { id: 3, name: </span><span style="background: white; color: #a31515;">"Bob3" </span><span style="background: white; color: black;">},
                    { id: 4, name: </span><span style="background: white; color: #a31515;">"Bob4" </span><span style="background: white; color: black;">},
                    { id: 5, name: </span><span style="background: white; color: #a31515;">"Bob5" </span><span style="background: white; color: black;">},
                    { id: 6, name: </span><span style="background: white; color: #a31515;">"Bob6" </span><span style="background: white; color: black;">},
                    { id: 7, name: </span><span style="background: white; color: #a31515;">"Bob7" </span><span style="background: white; color: black;">},
                    { id: 8, name: </span><span style="background: white; color: #a31515;">"Bob8" </span><span style="background: white; color: black;">},
                    { id: 9, name: </span><span style="background: white; color: #a31515;">"Bob9" </span><span style="background: white; color: black;">},
                    { id: 10, name: </span><span style="background: white; color: #a31515;">"Bob10" </span><span style="background: white; color: black;">},
                    { id: 11, name: </span><span style="background: white; color: #a31515;">"Bob11" </span><span style="background: white; color: black;">},
                    { id: 12, name: </span><span style="background: white; color: #a31515;">"Bob12" </span><span style="background: white; color: black;">}
                ]


                $scope.mainGridOptions = {
                    dataSource: {
                        data: data,
                        pageSize: 4
                    },
                    pageable: {
                        pageSizes: [4, 8, 12]
                    },
                    sortable: </span><span style="background: white; color: blue;">true</span><span style="background: white; color: black;">,
                    dataBinding: </span><span style="background: white; color: blue;">function </span><span style="background: white; color: black;">(e) {
                        </span><span style="background: white; color: green;">// This is a fix.
                        // When the user selects an other page size in the "page size" dropdownlist, 
                        // the MainGridOptions are not updated.
                        // To reflect the changes from the "page size" dropdownlist, we set the "page size" manually here.
                        </span><span style="background: white; color: black;">$scope.mainGridOptions.dataSource.pageSize = e.sender.dataSource.pageSize();
                    }
                };

                $scope.setPageSize = </span><span style="background: white; color: blue;">function </span><span style="background: white; color: black;">() {
                    $scope.mainGridOptions.dataSource.pageSize = data.length;
                };
            };

            app.controller(</span><span style="background: white; color: #a31515;">"main"</span><span style="background: white; color: black;">, [</span><span style="background: white; color: #a31515;">"$scope"</span><span style="background: white; color: black;">, controller]);
        }());
    </span><span style="background: white; color: blue;">&lt;/</span><span style="background: white; color: maroon;">script</span><span style="background: white; color: blue;">&gt;</span></pre>
<pre class="code"><span style="background: white; color: blue;">&lt;</span><span style="background: white; color: maroon;">div </span><span style="background: white; color: red;">ng-controller</span><span style="background: white; color: blue;">="main"&gt;
        &lt;</span><span style="background: white; color: maroon;">h2</span><span style="background: white; color: blue;">&gt;</span><span style="background: white; color: black;">{{ </span><span style="background: white; color: purple;">title </span><span style="background: white; color: black;">}}</span><span style="background: white; color: blue;">&lt;/</span><span style="background: white; color: maroon;">h2</span><span style="background: white; color: blue;">&gt;
        &lt;</span><span style="background: white; color: maroon;">div</span><span style="background: white; color: blue;">&gt;
            &lt;</span><span style="background: white; color: maroon;">br </span><span style="background: white; color: blue;">/&gt;
            &lt;</span><span style="background: white; color: maroon;">button </span><span style="background: white; color: red;">ng-click</span><span style="background: white; color: blue;">="setPageSize()"&gt;</span><span style="background: white; color: black;">Set page size</span><span style="background: white; color: blue;">&lt;/</span><span style="background: white; color: maroon;">button</span><span style="background: white; color: blue;">&gt;
            &lt;</span><span style="background: white; color: maroon;">br </span><span style="background: white; color: blue;">/&gt;
            &lt;</span><span style="background: white; color: maroon;">br </span><span style="background: white; color: blue;">/&gt;
            &lt;</span><span style="background: white; color: maroon;">div </span><span style="background: white; color: red;">kendo-grid</span><span style="background: white; color: blue;">="mainGrid"
                 </span><span style="background: white; color: red;">k-options</span><span style="background: white; color: blue;">="mainGridOptions"
                 </span><span style="background: white; color: red;">k-rebind</span><span style="background: white; color: blue;">="mainGridOptions"&gt;&lt;/</span><span style="background: white; color: maroon;">div</span><span style="background: white; color: blue;">&gt;
        &lt;/</span><span style="background: white; color: maroon;">div</span><span style="background: white; color: blue;">&gt;
    &lt;/</span><span style="background: white; color: maroon;">div</span><span style="background: white; color: blue;">&gt;</span></pre>
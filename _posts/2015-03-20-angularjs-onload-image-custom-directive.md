---
ID: 4300
post_title: AngularJS onload image custom directive
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/03/20/angularjs-onload-image-custom-directive/
published: true
post_date: 2015-03-20 08:04:35
---
<p>If you want to execute some code, when an image is fully loaded, you can use an custom directive in AngularJS, something like:</p>  <pre class="code"><span style="background: white; color: black">(</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
    </span><span style="background: white; color: green">/// &lt;summary&gt;
    /// Bind to onload event, e.g. onload image.
    /// &lt;/summary&gt;
    </span><span style="background: white; color: #a31515">&quot;use strict&quot;</span><span style="background: white; color: black">;

    </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">directive() {
        
        </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">link($scope, $element, attrs) {

            $element.bind(</span><span style="background: white; color: #a31515">'load'</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {

                $scope.options.load($element[0]);
                
            });

        }

        </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">{
            restrict: </span><span style="background: white; color: #a31515">&quot;A&quot;</span><span style="background: white; color: black">,
            scope: {
                options: </span><span style="background: white; color: #a31515">&quot;=htoOnload&quot;
            </span><span style="background: white; color: black">},
            link: link
        };
    }

    angular
        .module(</span><span style="background: white; color: #a31515">&quot;hto&quot;</span><span style="background: white; color: black">)
        .directive(</span><span style="background: white; color: #a31515">&quot;htoOnload&quot;</span><span style="background: white; color: black">, [directive]);

}());</span></pre>

<p>Usage:</p>

<pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">img </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;locationImage&quot; </span><span style="background: white; color: red">ng-src</span><span style="background: white; color: blue">=&quot;</span><span style="background: white; color: black">{{ </span><span style="background: white; color: purple">app.locationImageUrl </span><span style="background: white; color: black">}}</span><span style="background: white; color: blue">&quot; </span><span style="background: white; color: red">hto-onload</span><span style="background: white; color: blue">=&quot;{ load: app.onLocationImageLoad }&quot; /&gt;</span></pre>


<p>The $scope contains an object “app” containing a function “onLocationImageLoad”.</p>

<p>The image is dynamically loaded by AngularJS, when the app.locationImageUrl changes.</p>
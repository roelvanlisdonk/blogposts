---
ID: 4416
post_title: 'Server side resource rendering with Angular and ASP .NET MVC: pass data from html to controller.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/06/19/server-side-resource-rendering-with-angular-and-asp-net-mvc-pass-data-from-html-to-controller/
published: true
post_date: 2015-06-19 11:56:24
---
<p>I wanted a ASP .NET MVC view (*.cshtml) to render on the server and pass the static text contained in the the ASP .NET project resource file to an Angular controller, so on the initial page request, all static data is returned to the client. Dynamic data, like grid content would then be requested by a separate JSON call.</p>  <p>The resource data is passed to the Angular controller by using ng-init.</p>  <p>&#160;</p>  <p>For the sake of this blog post I stuffed everything in one *.cshtml page, including CSS en JavaScript.</p>  <p>Of course this would be separate files in an real application.</p>  <p>&#160;</p>   <p>Project resource file</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/06/image11.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/06/image_thumb11.png" width="580" height="114" /></a></p>  <p>&#160;</p>  <p><strong>Layout.cshtml</strong></p>  <p>&#160;</p>  <pre class="code"><p><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">!DOCTYPE </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">html </span><span style="background: white; color: red">xmlns:ng</span><span style="background: white; color: blue">=&quot;http://angularjs.org&quot; </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;ng-app&quot; </span><span style="background: white; color: red">ng-app</span><span style="background: white; color: blue">=&quot;app&quot;&gt;
&lt;</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">charset</span><span style="background: white; color: blue">=&quot;utf-8&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">http-equiv</span><span style="background: white; color: blue">=&quot;X-UA-Compatible&quot; </span><span style="background: white; color: red">content</span><span style="background: white; color: blue">=&quot;IE=edge&quot;&gt;
    &lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">name</span><span style="background: white; color: blue">=&quot;viewport&quot; </span><span style="background: white; color: red">content</span><span style="background: white; color: blue">=&quot;width=device-width, initial-scale=1.0&quot;&gt;
    &lt;</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">Send initialization data from HTML to Angular controller</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;
        </span><span style="background: white; color: #006400">/* Add some initial styling. */
        </span><span style="background: white; color: maroon">html</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">body </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">background-color</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">#F1F1F1</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">font-family</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">&quot;Open Sans&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">sans-serif</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">font-size</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">13px</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">100%</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: maroon">body </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">margin</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">20px</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: maroon">[ng\:cloak]</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">[ng-cloak]</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">[data-ng-cloak]</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">[x-ng-cloak]</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">.ng-cloak</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">.x-ng-cloak </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">display</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">none !important</span><span style="background: white; color: black">;
        }
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;

    </span><span style="background: white; color: #006400">&lt;!-- Library scripts --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;https://code.angularjs.org/1.4.1/angular.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body </span><span style="background: white; color: red">ng-cloak</span><span style="background: white; color: blue">&gt;
    </span><span style="background: yellow; color: black">@</span><span style="background: white; color: black">RenderBody()
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">div 
            </span><span style="background: white; color: red">ng-controller</span><span style="background: white; color: blue">=&quot;main&quot;
            </span><span style="background: white; color: red">ng-init</span><span style="background: white; color: blue">=&quot;resources={ textFromResource: '</span><span style="background: yellow; color: black">@</span><span style="background: white; color: black">WebApplication1.Properties.</span><span style="background: white; color: #2b91af">Resources</span><span style="background: white; color: black">.TextFromResource</span><span style="background: white; color: blue">'}&quot;&gt;
            &lt;</span><span style="background: white; color: maroon">h1</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">{{ </span><span style="background: white; color: purple">title </span><span style="background: white; color: black">}}</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">h1</span><span style="background: white; color: blue">&gt;
             </span><span style="background: white; color: black">{{ </span><span style="background: white; color: purple">resources.textFromResource </span><span style="background: white; color: black">}}
        </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
        </span><span style="background: white; color: green">// Angular module.
        </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
        {
            </span><span style="background: white; color: #a31515">&quot;use strict&quot;</span><span style="background: white; color: black">;

            angular
                .module(</span><span style="background: white; color: #a31515">&quot;app&quot;</span><span style="background: white; color: black">, []);
        }());

        </span><span style="background: white; color: green">// Angular controller.
        </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
        {
            </span><span style="background: white; color: #a31515">&quot;use strict&quot;</span><span style="background: white; color: black">;

            </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">controller($scope)
            {
                $scope.title = </span><span style="background: white; color: #a31515">&quot;Show ASP .NET MVC resoure (*.resx) data to user on initial load.&quot;</span><span style="background: white; color: black">;                
            }

            angular
                .module(</span><span style="background: white; color: #a31515">&quot;app&quot;</span><span style="background: white; color: black">)
                .controller(</span><span style="background: white; color: #a31515">&quot;main&quot;</span><span style="background: white; color: black">, [</span><span style="background: white; color: #a31515">&quot;$scope&quot;</span><span style="background: white; color: black">, controller]);
        }());
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
</span></p></pre>


<p>&#160;</p>

<p>&#160;</p>

<p><strong>Result</strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/06/image12.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/06/image_thumb12.png" width="580" height="124" /></a></p>
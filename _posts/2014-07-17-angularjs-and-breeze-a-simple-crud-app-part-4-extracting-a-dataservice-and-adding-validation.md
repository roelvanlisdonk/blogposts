---
ID: 3981
post_title: 'AngularJS and Breeze &ndash; A simple crud app &ndash; Part 4 &ndash; Extracting a data service and adding validation.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/07/17/angularjs-and-breeze-a-simple-crud-app-part-4-extracting-a-dataservice-and-adding-validation/
published: true
post_date: 2014-07-17 13:15:27
---
<p>&#160;</p>  <p>In this post all will be extracting a data service from the code created in the previous posts and I will be adding some client side validation by using the breeze directive: data-z-validate.</p>  <p>&#160;</p>  <p><strong>Note</strong></p>  <p>All code can be found at:</p>  <p><a href="https://github.com/roelvanlisdonk/Research/tree/master/Research/Research.UI.Web/Client/Features/AngularJS_and_Breeze/Part4">https://github.com/roelvanlisdonk/Research/tree/master/Research/Research.UI.Web/Client/Features/AngularJS_and_Breeze/Part4</a></p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image25.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image_thumb25.png" width="580" height="177" /></a></p>  <p>&#160;</p>  <p>Just by adding the data-z-validate attribute to the input elements in the grid, breeze will automatically show client side validation errors, by default an asterisk “*” is shown for required fields and a message is shown, when the user clears a required field. </p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image26.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image_thumb26.png" width="580" height="177" /></a></p>  <p>&#160;</p>  <p>In this case I also added a maxlength data annotation to the lastName field:</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image27.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image_thumb27.png" width="580" height="129" /></a></p>  <p>&#160;</p>  <p><strong>Model</strong></p>  <pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">Research.UI.Web.Server.Model
{
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.ComponentModel.DataAnnotations;

    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">Employee
    </span><span style="background: white; color: black">{
        [</span><span style="background: white; color: #2b91af">Key</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public int </span><span style="background: white; color: black">Id { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        [</span><span style="background: white; color: #2b91af">Required</span><span style="background: white; color: black">]
        [</span><span style="background: white; color: #2b91af">MaxLength</span><span style="background: white; color: black">(20)]
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">FirstName { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        [</span><span style="background: white; color: #2b91af">Required</span><span style="background: white; color: black">]
        [</span><span style="background: white; color: #2b91af">MaxLength</span><span style="background: white; color: black">(50)]
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">LastName { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
        [</span><span style="background: white; color: #2b91af">MaxLength</span><span style="background: white; color: black">(20)]
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">PhoneNumber { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
    }
}</span></pre>

<p><strong>Note</strong></p>

<p>I encountered a problem with the data-z-validate directive, this was caused by added the directive dynamically in a custom directive created by me, see: <a title="http://stackoverflow.com/questions/22849402/angular-directive-with-a-template-does-not-work-with-z-validate" href="http://stackoverflow.com/questions/22849402/angular-directive-with-a-template-does-not-work-with-z-validate">http://stackoverflow.com/questions/22849402/angular-directive-with-a-template-does-not-work-with-z-validate</a> but this was fixed by altering my custom directive.</p>

<p>&#160;</p>

<p><strong>The custom directive with fix</strong></p>

<pre class="code"><span style="background: white; color: green">// Angular directive [spaField] responsible for generating grid cell controls.
</span><span style="background: white; color: black">spa.app.directive(</span><span style="background: white; color: #a31515">'spaField'</span><span style="background: white; color: black">, [</span><span style="background: white; color: #a31515">'$compile'</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">($compile)
{
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">directive = {
        restrict: </span><span style="background: white; color: #a31515">'A'</span><span style="background: white; color: black">, </span><span style="background: white; color: green">/* Restrict this directive to attributes.  */
        </span><span style="background: white; color: black">replace: </span><span style="background: white; color: blue">true</span><span style="background: white; color: black">, </span><span style="background: white; color: green">/* The given element will be replaced in the link function. */
        </span><span style="background: white; color: black">link: </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">($scope, element, attrs)
        {
            </span><span style="background: white; color: green">// The data-z-validate directive will append a [span class=&quot;z-decorator&quot;] to the following [input] element, by using the jquery &quot;append&quot; function.
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">html = </span><span style="background: white; color: #a31515">'&lt;input ng-disabled=&quot;{{vm.isKeyField(prop)}}&quot; type=&quot;text&quot; data-ng-model=&quot;entity[prop.name]&quot; data-z-validate&gt;'</span><span style="background: white; color: black">;

            </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">($scope.prop.relatedNavigationProperty) {
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">relatedTableName = $scope.prop.relatedNavigationProperty.nameOnServer;
                html = </span><span style="background: white; color: #a31515">'&lt;select kendo-combo-box ng-model=&quot;entity[prop.name]&quot; ng-options=&quot;record.id as record.firstName for record in vm[\'' </span><span style="background: white; color: black">+ relatedTableName + </span><span style="background: white; color: #a31515">'\']&quot;&gt;&lt;/select&gt;'</span><span style="background: white; color: black">;
            } </span><span style="background: white; color: blue">else if </span><span style="background: white; color: black">($scope.prop.dataType.name === </span><span style="background: white; color: #a31515">&quot;DateTime&quot;</span><span style="background: white; color: black">) {
                html = </span><span style="background: white; color: #a31515">'&lt;input kendo-date-picker k-ng-model=&quot;entity[prop.name]&quot; k-format=&quot;\'dd-MMM-yyyy\'&quot; /&gt;'</span><span style="background: white; color: black">;
            } </span><span style="background: white; color: blue">else if </span><span style="background: white; color: black">($scope.prop.dataType.name === </span><span style="background: white; color: #a31515">&quot;Boolean&quot;</span><span style="background: white; color: black">)
            {
                html = </span><span style="background: white; color: #a31515">'&lt;input kendo-mobile-switch k-on-label=&quot;\'YES\'&quot; k-off-label=&quot;\'NO\'&quot; /&gt;'</span><span style="background: white; color: black">;
            }

            </span><span style="background: white; color: green">// Apply scope to the created html fragment.
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">compiled = $compile(html)($scope);

            </span><span style="background: white; color: green">// Get the [&lt;span class=&quot;z-decorator&quot;] appended to the input element by the z-validate directive.
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">span = compiled[0].parentNode.children[1];

            </span><span style="background: white; color: green">// The following 2 lines will only add the input element to the DOM and not the [span class=&quot;z-decorator&quot;], that is added by the z-validate directive.
            </span><span style="background: white; color: black">element.replaceWith(compiled);
            element = compiled;

            </span><span style="background: white; color: green">// Add the [span class=&quot;z-decorator&quot;] to the current parent element of the input element.
            </span><span style="background: white; color: black">element.parent().append(span);
            element.parent().append(span);
        }
    };
    
    </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">directive;
}]);</span></pre>
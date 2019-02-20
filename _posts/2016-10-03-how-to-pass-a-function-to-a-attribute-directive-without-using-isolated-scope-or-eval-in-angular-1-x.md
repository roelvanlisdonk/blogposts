---
ID: 4994
post_title: >
  How to pass a function to an attribute
  directive, without using isolated scope
  or eval in Angular 1.x
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2016/10/03/how-to-pass-a-function-to-a-attribute-directive-without-using-isolated-scope-or-eval-in-angular-1-x/
published: true
post_date: 2016-10-03 23:05:33
---
<p><font size="3"></font></p>  <p><font size="3">I have created a little POC to demonstrate, how you can pass a function that resides on the scope, to be passed to a attribute directive without using isolated scope or eval in Angular 1.x.</font></p>  <p><font size="3">The first button will be focused when the page is loaded.</font></p>  <p><font size="3">When you tab on the first button, the default tab action is applied, so the second button is focused.</font></p>  <p><font size="3">When you tab on the second button the function, that was passed to the “tab directive” is called. It will set a message on the scope.</font>&#160;</p>        <p><a href="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/10/image.png" rel="lightbox"><img title="image" style="margin: 0px; display: inline; background-image: none;" border="0" alt="image" src="https://www.roelvanlisdonk.nl/wp-content/uploads/2016/10/image_thumb.png" width="244" height="227" /></a></p>  <p>&#160; </p>        <pre>namespace poc {
    'use strict';
        
    const app = angular.module('poc', []);

    class PocDirective implements ng.IDirective {
        public link: ($scope: IPocScope, $element: ng.IAugmentedJQuery, attrs: ng.IAttributes) =&gt; void;
        public restrict = 'E';
        public template = `</pre>

<p>&lt;action-button&gt;
  <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &lt;button id=&quot;button-1&quot; type=&quot;button&quot;&gt;Tab on this button&lt;/button&gt;

  <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; &lt;/action-button&gt;

  <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; &lt;action-button&gt;

  <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &lt;button poc-tab=&quot;{ fn: onTab }&quot; type=&quot;button&quot;&gt;Tab on this button&lt;/button&gt;

  <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; &lt;/action-button&gt;

  <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; &lt;div ng-bind=&quot;message&quot;&gt;&lt;/div&gt;</p>

<pre>`;

        constructor(public $timeout:ng.ITimeoutService) {
            const self: PocDirective = this;
            
            self.link = self.unboundLink.bind(self);
        }

        unboundLink($scope: IPocScope, $element: ng.IAugmentedJQuery, attrs: ng.IAttributes) {
            const self: PocDirective = this;

            function onTab(){
                $scope.message = &quot;Tabbed on button&quot;;
            }
                   
            self.$timeout(function() {
               const button1 = document.getElementById('button-1');
               button1.focus();
            });

            $scope.onTab = onTab;
        }
    }

    interface IPocScope extends ng.IScope {
        message: string;
        onTab: () =&gt; void;
    }

    app.directive('poc', ['$timeout', ($timeout) =&gt; new PocDirective($timeout)]);

    function safeApply($scope: ng.IScope): boolean {
        var result = false;

        var phase = $scope.$root.$$phase;
        if (phase !== '$apply' &amp;&amp; phase !== '$digest') {
            $scope.$apply();
            result = true;
        }

        return result;
    }

    /**
     * We want to able to use this directive in association with other directives on the same element.
     * So we don't use isolated scope, to prevent the error:
     *      &quot;Multiple directives [..., ...] asking for new/isolated scope on: ...&quot;.
     * But we want to be able to pass a function to this directive from outside, 
     * that's why we parse the value of the &quot;poc-tab&quot; attribute.
     */
    class TabDirective implements ng.IDirective {
        public link: (scope: ng.IScope, element: ng.IAugmentedJQuery, attrs: ITabAttributes) =&gt; void;
        public restrict = 'A';

        constructor(public $parse: ng.IParseService) {
            const self: TabDirective = this;

            self.link = self.unboundLink.bind(self);
        }

        unboundLink(scope: ng.IScope, element: ng.IAugmentedJQuery, attrs: ITabAttributes) {
            const self: TabDirective = this;
            
            element.bind('keydown keypress', function (event) {
                const tabKey = 9;
                const tabIsPressed = (event.which === tabKey); 
                if (tabIsPressed) {
                    const optionsAsString: string = attrs.pocTab;
                    const optionsAsExpression: ng.ICompiledExpression = self.$parse(optionsAsString);
                    const options: ITabOptions = optionsAsExpression(scope);

                    options.fn();
                    safeApply(scope);
                    event.preventDefault();
                }
            });
        }
    }

    interface ITabAttributes extends ng.IAttributes {
        pocTab: string;
    }

    export interface ITabOptions {
        fn: () =&gt; void;
        ignore?: boolean; // When true, given fn is NOT executed.
    }

    app.directive('pocTab', ['$parse', ($parse) =&gt; new TabDirective($parse)]);
    
    angular.bootstrap(document, ['poc']);
}




</pre>
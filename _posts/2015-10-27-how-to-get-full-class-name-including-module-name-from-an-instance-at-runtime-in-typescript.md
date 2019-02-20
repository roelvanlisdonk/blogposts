---
ID: 4659
post_title: >
  How to get full class name, including
  module name from an instance at runtime
  in TypeScript
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/10/27/how-to-get-full-class-name-including-module-name-from-an-instance-at-runtime-in-typescript/
published: true
post_date: 2015-10-27 13:07:45
---
<p>Let’s assume we have the class [GuidGenerator] in a TypeScript module [research.my.long.namespace] and at runtime you have an instance of the GuidGenerator, how do you get the full class name including module name, in this case: “research.my.long.namespace.GuidGenerator”.</p>  <p>Well you walk the object graph starting with the root / global object, in the browser this will be the window object.</p>  <p>&#160;</p>  <p>NOTE: all code is in “strict” modus.</p>  <p>&#160;</p>  <p><strong></strong></p>  <p><strong>TypeScript Class [GuidGenerator]:</strong></p>  <pre class="code"><span style="background: white; color: black">module research.my.long.namespace {
    &quot;use strict&quot;;

    export interface IGuidGenerator {
        generate(): string;
    }

    export class GuidGenerator implements IGuidGenerator {
        generate() {
            var randomNumberToGuid = function (c) {
                var r = Math.random() * 16 | 0, v = c == 'x' ? r : r &amp; 0x3 | 0x8;
                return v.toString(16);
            }
            return 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, randomNumberToGuid);
        }
    }
}</span></pre>

<p>We use the resolver object to get the full class name:</p>

<pre class="code"><span style="background: white; color: black">var resolver = new NameResolver();
var generator = new research.my.long.namespace.GuidGenerator();
var name = resolver.getFullClassNameFromInstance(generator, window)
console.log(name);</span></pre>

<p><strong>Result</strong></p>
<a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/10/image2.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2015/10/image_thumb2.png" width="580" height="110" /></a>



<p><strong>The resolver class</strong></p>

<pre class="code"><span style="background: white; color: black">module research.metadata {
    &quot;use strict&quot;;

    interface IProcessResult {
        fnFound: boolean;
        path: Array&lt;string&gt;;
    }

    export interface INameResolver {
        getFullClassNameFromInstance(instance: any, global: any): string;
    }

    export class NameResolver implements INameResolver {
        private _fn: any;
        private _global: any;
        private _processed: Array&lt;any&gt;;

        /**
            To handle recursiveness in the object graph, collect all handled nodes in the object graph,
            so an object is only traversed once.
        */
        isProcessed(obj: any): boolean {
            var result = false;
            for (var i, length; i &lt; length; i += 1) {
                if (this._processed[i] === obj) {
                    return true;
                }
            }
            return result;
        }

        processProperty(obj: any, key: string, path: Array&lt;string&gt;): IProcessResult {
            var result: IProcessResult = {
                fnFound: false,
                path: path
            }

            if (obj.hasOwnProperty(key)) {
                try {
                    var prop = obj[key];
                    if (prop === this._fn) {
                        // Function found, stop traversing the object graph.
                        result.fnFound = true;
                        return result;
                    }
                    
                    // Continue traversing the object graph.
                    result = this.processObject(prop, path);

                    if (result.fnFound) {
                        // Function found, stop traversing the object graph.
                        return result;
                    }
                } catch (error) {
                    // Access to some properties result in exceptions.
                }
            }
            

            return result;
        }

        processObject(obj: any, path: Array&lt;string&gt;): IProcessResult {
            var result: IProcessResult = {
                fnFound: false,
                path: path
            }

            if (this.isProcessed(obj)) {
                return result;
            }
            this._processed.push(obj);
            
            for (var key in obj) {
                var pathCopy = path.slice();
                pathCopy.push(key);
                var processResult = this.processProperty(obj, key, pathCopy);
                if (processResult.fnFound) {
                    return processResult;
                }
            }

            return processResult;
        }

        getFullClassNameFromInstance(instance: any, global: any): string {
            this._fn = instance[&quot;constructor&quot;];
            this._global = global;
            this._processed = [];

            var processResult = this.processObject(this._global, []);

            var fullFnName = &quot;&quot;;
            if (processResult.fnFound) {
                fullFnName = processResult.path.join(&quot;.&quot;);
            }

            return fullFnName;
        }
    }
}</span></pre>
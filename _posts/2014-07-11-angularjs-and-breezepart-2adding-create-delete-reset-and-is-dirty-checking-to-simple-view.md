---
ID: 3949
post_title: 'AngularJS and Breeze &ndash; A simple crud app &ndash; Part 2 &ndash; Adding create, delete, reset and is dirty checking.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/07/11/angularjs-and-breezepart-2adding-create-delete-reset-and-is-dirty-checking-to-simple-view/
published: true
post_date: 2014-07-11 14:31:19
---
<p>&#160;</p>  <p>In my previous <a href="http://www.roelvanlisdonk.nl/?p=3937">post</a> I created a simple [AngularJS – Breeze] edit view. In this post I will add the create, delete, reset and “is dirty” (entity change state tracking) to the simple view.</p>  <p>&#160;</p>  <p><strong>Before create</strong></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image17.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image_thumb17.png" width="580" height="333" /></a></p>  <p>&#160;</p>  <p><strong>Create</strong></p>  <p>The user clicked on the create button, so an “is dirty” icon is shown and a new row is added to the grid.</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image18.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image_thumb18.png" width="580" height="340" /></a></p>  <p>&#160;</p>  <p><strong>Save</strong></p>  <p>When the user fills the fields of the new row and clicks save, the “is dirty” icon will disappear and the id field will automatically be filled by the id generated on the server in the database.</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image19.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image_thumb19.png" width="580" height="333" /></a></p>  <p>&#160;</p>  <p><strong>Reset</strong></p>  <p>When the user create, updated and deleted some records and pressed save, the original state of the database can be restored by pressing the reset button.</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image20.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image_thumb20.png" width="580" height="316" /></a></p>  <p>&#160;</p>  <p>&#160;</p>  <p><strong>index.html</strong></p>  <pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">!DOCTYPE </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">html </span><span style="background: white; color: red">data-ng-app</span><span style="background: white; color: blue">=&quot;app&quot;&gt;
&lt;</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">title </span><span style="background: white; color: red">data-ng-bind</span><span style="background: white; color: blue">=&quot;title&quot;&gt;</span><span style="background: white; color: black">Angular and Breeze</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">charset</span><span style="background: white; color: blue">=&quot;utf-8&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">http-equiv</span><span style="background: white; color: blue">=&quot;X-UA-Compatible&quot; </span><span style="background: white; color: red">content</span><span style="background: white; color: blue">=&quot;IE=edge, chrome=1&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">name</span><span style="background: white; color: blue">=&quot;viewport&quot; </span><span style="background: white; color: red">content</span><span style="background: white; color: blue">=&quot;width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalable=no&quot; /&gt;

    </span><span style="background: white; color: #006400">&lt;!-- Libraries --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot; </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;../../../Libraries/FontAwesome/css/font-awesome.min.css&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot; </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;../../../Libraries/Toastr/toastr.min.css&quot; /&gt;
    </span><span style="background: white; color: blue">
    </span><span style="background: white; color: #006400">&lt;!-- App --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot; </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;app.css&quot; /&gt;
&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;spa-page&quot; </span><span style="background: white; color: red">data-ng-controller</span><span style="background: white; color: blue">=&quot;admin as vm&quot;&gt;
        &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;spa-grid-toolbar&quot;&gt;
            &lt;</span><span style="background: white; color: maroon">a </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;spa-action-link&quot; </span><span style="background: white; color: red">ng-click</span><span style="background: white; color: blue">=&quot;vm.save()&quot;&gt;</span><span style="background: white; color: black">save</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">a</span><span style="background: white; color: blue">&gt; </span><span style="background: white; color: black">|
            </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">a </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;spa-action-link&quot; </span><span style="background: white; color: red">ng-click</span><span style="background: white; color: blue">=&quot;vm.reset()&quot;&gt;</span><span style="background: white; color: black">reset</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">a</span><span style="background: white; color: blue">&gt; </span><span style="background: white; color: black">|
            </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">a </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;spa-action-link&quot; </span><span style="background: white; color: red">ng-click</span><span style="background: white; color: blue">=&quot;vm.create()&quot;&gt;</span><span style="background: white; color: black">create</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">a</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">i </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;fa fa-exclamation-circle&quot; 
               </span><span style="background: white; color: red">title</span><span style="background: white; color: blue">=&quot;Some data has change. Press save to save the changes to the server!&quot; 
               </span><span style="background: white; color: red">ng-show</span><span style="background: white; color: blue">=&quot;vm.isDirty&quot;&gt;&lt;/</span><span style="background: white; color: maroon">i</span><span style="background: white; color: blue">&gt;
        &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">table </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;spa-grid&quot;&gt;
            &lt;</span><span style="background: white; color: maroon">thead</span><span style="background: white; color: blue">&gt;
                &lt;</span><span style="background: white; color: maroon">tr</span><span style="background: white; color: blue">&gt;
                    &lt;</span><span style="background: white; color: maroon">th</span><span style="background: white; color: blue">&gt; &lt;/</span><span style="background: white; color: maroon">th</span><span style="background: white; color: blue">&gt;
                    &lt;</span><span style="background: white; color: maroon">th </span><span style="background: white; color: red">ng-repeat</span><span style="background: white; color: blue">='(key, prop) in vm.entityFields'&gt;</span><span style="background: white; color: black">{{ </span><span style="background: white; color: purple">prop.name </span><span style="background: white; color: black">}}</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">th</span><span style="background: white; color: blue">&gt;
                &lt;/</span><span style="background: white; color: maroon">tr</span><span style="background: white; color: blue">&gt;
            &lt;/</span><span style="background: white; color: maroon">thead</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">tbody</span><span style="background: white; color: blue">&gt;
                &lt;</span><span style="background: white; color: maroon">tr </span><span style="background: white; color: red">ng-repeat</span><span style="background: white; color: blue">=&quot;entity in vm.entities&quot;&gt;
                    &lt;</span><span style="background: white; color: maroon">td</span><span style="background: white; color: blue">&gt;&lt;</span><span style="background: white; color: maroon">a </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;spa-action-link&quot; </span><span style="background: white; color: red">ng-click</span><span style="background: white; color: blue">=&quot;vm.delete(entity)&quot;&gt;</span><span style="background: white; color: black">delete</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">a</span><span style="background: white; color: blue">&gt;&lt;/</span><span style="background: white; color: maroon">td</span><span style="background: white; color: blue">&gt;
                    &lt;</span><span style="background: white; color: maroon">td </span><span style="background: white; color: red">ng-repeat</span><span style="background: white; color: blue">='(key, prop) in vm.entityFields'&gt;
                        &lt;</span><span style="background: white; color: maroon">input </span><span style="background: white; color: red">ng-disabled</span><span style="background: white; color: blue">=&quot;{{vm.isReadOnlyField(prop.name)}}&quot; 
                               </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">='text' 
                               </span><span style="background: white; color: red">ng-model</span><span style="background: white; color: blue">='entity[prop.name]'&gt;
                    &lt;/</span><span style="background: white; color: maroon">td</span><span style="background: white; color: blue">&gt;
                &lt;/</span><span style="background: white; color: maroon">tr</span><span style="background: white; color: blue">&gt;
            &lt;/</span><span style="background: white; color: maroon">tbody</span><span style="background: white; color: blue">&gt;
        &lt;/</span><span style="background: white; color: maroon">table</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;

    </span><span style="background: white; color: #006400">&lt;!-- Libraries --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;../../../Libraries/Angular/angular.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;../../../Libraries/Breeze/breeze.debug.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;../../../Libraries/Breeze/breeze.angular.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;

    </span><span style="background: white; color: #006400">&lt;!-- Add toastr which needs jQuery (Breeze does not need jQuery) --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;../../../Libraries/jQuery/jquery-2.1.1.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;../../../Libraries/Toastr/toastr.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    <br /></span><span style="background: white; color: #006400">    &lt;!-- Add breeze.savequeuing which needs Q (Breeze does not need Q)--&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;../../../Libraries/Q/q.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;../../../Libraries/Breeze/breeze.savequeuing.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;

    </span><span style="background: white; color: #006400">&lt;!-- App --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;app.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
</span></pre>

<p>&#160;</p>

<p>&#160;</p>

<p><strong>app.js</strong></p>

<pre class="code"><span style="background: white; color: green">// Use namespaces to prevent pollution of the global namespace.
</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">spa = spa || {};
spa.controllers = spa.controllers || {};

</span><span style="background: white; color: green">// Angular module [app].
</span><span style="background: white; color: black">spa.app = (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
    </span><span style="background: white; color: #a31515">'use strict'</span><span style="background: white; color: black">;

    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">app = angular.module(</span><span style="background: white; color: #a31515">'app'</span><span style="background: white; color: black">, [
        </span><span style="background: white; color: #a31515">'breeze.angular' </span><span style="background: white; color: green">// The breeze service module.
    </span><span style="background: white; color: black">]);
})();

</span><span style="background: white; color: green">// Angular controller [admin].
</span><span style="background: white; color: black">spa.controllers.admin = (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
    </span><span style="background: white; color: #a31515">'use strict'</span><span style="background: white; color: black">;
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">controllerId = </span><span style="background: white; color: #a31515">'admin'</span><span style="background: white; color: black">;
    angular.module(</span><span style="background: white; color: #a31515">'app'</span><span style="background: white; color: black">).controller(controllerId, [</span><span style="background: white; color: #a31515">'$http'</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">'breeze'</span><span style="background: white; color: black">, admin]);

    </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">admin($http, breeze) {
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">entityChangedToken = </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">;
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">entityTypeName = </span><span style="background: white; color: #a31515">&quot;Employee&quot;</span><span style="background: white; color: black">;
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">manager = </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">;

        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">vm = </span><span style="background: white; color: blue">this</span><span style="background: white; color: black">;
        vm.create = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
            </span><span style="background: white; color: green">// Create entity by breeze.
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">entity = manager.createEntity(entityTypeName);
            </span><span style="background: white; color: green">// Show entity to user.
            </span><span style="background: white; color: black">vm.entities.push(entity);
        };
        vm.delete = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(entity) {
            </span><span style="background: white; color: green">// Delete from UI
            </span><span style="background: white; color: black">vm.entities.pop(entity);

            </span><span style="background: white; color: green">// Mark for deletion.
            </span><span style="background: white; color: black">entity.entityAspect.setDeleted();
        };
        vm.entities = [];
        vm.entityFields = </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">;
        vm.isDirty = </span><span style="background: white; color: blue">false</span><span style="background: white; color: black">;
        vm.isReadOnlyField = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(name) {
            </span><span style="background: white; color: green">// Make 'id' fields read-only.
            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">(name === </span><span style="background: white; color: #a31515">'id'</span><span style="background: white; color: black">);
        };
        vm.reset = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
            </span><span style="background: white; color: green">// Re-seed database and refetch data.
            </span><span style="background: white; color: black">$http.get(</span><span style="background: white; color: #a31515">'/breeze/breeze/ReSeed'</span><span style="background: white; color: black">).then(getData).then(handleResetResult).catch(showError);
        };
        vm.save = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
            manager.saveChanges().then(handleSaveResult).catch(showError);
        };

        </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">handleStateChange(args) {
            vm.isDirty = </span><span style="background: white; color: blue">true</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">getData() {
            </span><span style="background: white; color: green">// Get entities from the server.
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">query = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">breeze.EntityQuery().from(entityTypeName);
            manager.executeQuery(query).then(handleGetDataResult).catch(showError);
        }

        </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">initialize() {
            </span><span style="background: white; color: green">// Use camel case for entity properties.
            </span><span style="background: white; color: black">breeze.NamingConvention.camelCase.setAsDefault();

            </span><span style="background: white; color: green">// Configure and create EntityManager (double breeze is needed, because of .
            </span><span style="background: white; color: black">manager = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">breeze.EntityManager(</span><span style="background: white; color: #a31515">'/breeze/breeze'</span><span style="background: white; color: black">);
            manager.enableSaveQueuing(</span><span style="background: white; color: blue">true</span><span style="background: white; color: black">);
            registerForStateChange();

            getData();
        }

        </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">handleGetDataResult(data) {
            </span><span style="background: white; color: green">// Get entity fields from metadata.
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">entityMetaData = manager.metadataStore.getEntityType(entityTypeName);
            vm.entityFields = entityMetaData.dataProperties;

            </span><span style="background: white; color: green">// Show the enties from the server.
            </span><span style="background: white; color: black">vm.entities = data.results;
            vm.isDirty = </span><span style="background: white; color: blue">false</span><span style="background: white; color: black">;
        }

        </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">handleResetResult() {
            vm.isDirty = </span><span style="background: white; color: blue">false</span><span style="background: white; color: black">;
            toastr.info(</span><span style="background: white; color: #a31515">&quot;Database re-seeded.&quot;</span><span style="background: white; color: black">);
        }

        </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">handleSaveResult() {
            vm.isDirty = </span><span style="background: white; color: blue">false</span><span style="background: white; color: black">;
            toastr.info(</span><span style="background: white; color: #a31515">&quot;Changes saved to the server.&quot;</span><span style="background: white; color: black">);
        }

        </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">registerForStateChange() {
            </span><span style="background: white; color: green">// Make sure to only subscribe once.
            </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(entityChangedToken) { </span><span style="background: white; color: blue">return</span><span style="background: white; color: black">; }

            </span><span style="background: white; color: green">// Register for state change.
            </span><span style="background: white; color: black">entityChangedToken = manager.entityChanged.subscribe(handleStateChange);
        }

        </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">showError(e) {
            </span><span style="background: white; color: green">// Show xhr error.
            </span><span style="background: white; color: black">toastr.error(e);
        }

        initialize();
    }
})();</span></pre>

<p>&#160;</p>

<p><strong>app.css</strong></p>

<pre class="code"><span style="background: white; color: #006400">/* Resets */
</span><span style="background: white; color: maroon">html</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">body</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">div</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">span</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">object</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">iframe</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">h1</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">h2</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">h3</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">h4</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">h5</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">h6</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">p</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">blockquote</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">pre</span><span style="background: white; color: black">,</span><span style="background: white; color: maroon">abbr</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">address</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">cite</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">code</span><span style="background: white; color: black">,
</span><span style="background: white; color: maroon">del</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">dfn</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">em</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">img</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">ins</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">kbd</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">q</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">samp</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">small</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">strong</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">sub</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">sup</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">var</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">b</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">i</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">dl</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">dt</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">dd</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">ol</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">ul</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">li</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">fieldset</span><span style="background: white; color: black">,
</span><span style="background: white; color: maroon">form</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">label</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">legend</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">table</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">caption</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">tbody</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">tfoot</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">thead</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">tr</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">th</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">td</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">article</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">aside</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">canvas</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">details</span><span style="background: white; color: black">, 
</span><span style="background: white; color: maroon">figcaption</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">figure</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">footer</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">header</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">hgroup</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">menu</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">nav</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">section</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">summary</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">time</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">mark</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">audio</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">video </span><span style="background: white; color: black">{
    </span><span style="background: white; color: red">border</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;              </span><span style="background: white; color: #006400">/* Prevent unnecessary white space. */
    </span><span style="background: white; color: red">-moz-box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">;
    </span><span style="background: white; color: red">-webkit-box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">;
    </span><span style="background: white; color: red">box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">; </span><span style="background: white; color: #006400">/*  Border boxing is used, so the padding, margin and borders are within 
                                the width and height of the element. */
    </span><span style="background: white; color: red">margin</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;              </span><span style="background: white; color: #006400">/* Prevent unnecessary white space. */
    </span><span style="background: white; color: red">outline</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;             </span><span style="background: white; color: #006400">/* Prevent unnecessary white space. */
    </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;             </span><span style="background: white; color: #006400">/* Prevent unnecessary white space. */
    </span><span style="background: white; color: red">font-size</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">100%</span><span style="background: white; color: black">;
    </span><span style="background: white; color: red">vertical-align</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">baseline</span><span style="background: white; color: black">;
}

</span><span style="background: white; color: maroon">html</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">body </span><span style="background: white; color: black">{
    </span><span style="background: white; color: red">height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">100%</span><span style="background: white; color: black">;       </span><span style="background: white; color: #006400">/* Full screen single page app. */
    </span><span style="background: white; color: red">max-height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">100%</span><span style="background: white; color: black">;   </span><span style="background: white; color: #006400">/* Full screen single page app. */
</span><span style="background: white; color: black">}

</span><span style="background: white; color: maroon">body </span><span style="background: white; color: black">{
    </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">20px</span><span style="background: white; color: black">;
}

</span><span style="background: white; color: maroon">a </span><span style="background: white; color: black">{
    </span><span style="background: white; color: red">cursor</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">pointer</span><span style="background: white; color: black">;
}

</span><span style="background: white; color: maroon">a.spa-action-link </span><span style="background: white; color: black">{
    </span><span style="background: white; color: red">color</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">#428bca</span><span style="background: white; color: black">;
    </span><span style="background: white; color: red">text-decoration</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">none</span><span style="background: white; color: black">;
}

</span><span style="background: white; color: maroon">a.spa-action-link:hover</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">a.spa-action-link:focus </span><span style="background: white; color: black">{
    </span><span style="background: white; color: red">color</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">#2a6496</span><span style="background: white; color: black">;
    </span><span style="background: white; color: red">text-decoration</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">underline</span><span style="background: white; color: black">;
}

</span><span style="background: white; color: maroon">div.spa-page </span><span style="background: white; color: black">{
    </span><span style="background: white; color: red">border</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">1px solid rgb(212, 212, 212)</span><span style="background: white; color: black">;
    </span><span style="background: white; color: red">height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">100%</span><span style="background: white; color: black">;       </span><span style="background: white; color: #006400">/* Full screen single page app. */
    </span><span style="background: white; color: red">max-height</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">100%</span><span style="background: white; color: black">;   </span><span style="background: white; color: #006400">/* Full screen single page app. */
    </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">20px</span><span style="background: white; color: black">;
    </span><span style="background: white; color: red">position</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">relative</span><span style="background: white; color: black">;
}

</span><span style="background: white; color: maroon">div.spa-page &gt; a </span><span style="background: white; color: black">{
    </span><span style="background: white; color: red">margin-bottom</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">10px</span><span style="background: white; color: black">;
}

</span><span style="background: white; color: maroon">div.spa-grid-toolbar i.fa-exclamation-circle </span><span style="background: white; color: black">{
    </span><span style="background: white; color: red">margin-left</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">10px</span><span style="background: white; color: black">;
}

</span><span style="background: white; color: maroon">.spa-grid input[type=&quot;text&quot;] </span><span style="background: white; color: black">{
    </span><span style="background: white; color: red">padding-left</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">2px</span><span style="background: white; color: black">;
}</span></pre>

<p>&#160;</p>

<p><strong>BreezeController.cs</strong></p>

<pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">Research.UI.Web.Server.Controllers
{
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Breeze.ContextProvider;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Breeze.ContextProvider.EF6;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Breeze.WebApi2;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Newtonsoft.Json.Linq;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Research.UI.Web.Server.Model;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Data.Entity.Migrations;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Linq;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Web.Http;

    [</span><span style="background: white; color: #2b91af">BreezeController</span><span style="background: white; color: black">]
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">BreezeController </span><span style="background: white; color: black">: </span><span style="background: white; color: #2b91af">ApiController
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">private readonly </span><span style="background: white; color: #2b91af">EFContextProvider</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">ResearchDbContext</span><span style="background: white; color: black">&gt; _contextProvider;

        </span><span style="background: white; color: blue">public </span><span style="background: white; color: black">BreezeController(): </span><span style="background: white; color: blue">this</span><span style="background: white; color: black">(</span><span style="background: white; color: blue">null</span><span style="background: white; color: black">)
        {
        }

        </span><span style="background: white; color: blue">public </span><span style="background: white; color: black">BreezeController(</span><span style="background: white; color: #2b91af">EFContextProvider</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">ResearchDbContext</span><span style="background: white; color: black">&gt; contextProvider)
        {
            _contextProvider = contextProvider ??  </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">EFContextProvider</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">ResearchDbContext</span><span style="background: white; color: black">&gt;();
        }

        [</span><span style="background: white; color: #2b91af">HttpGet</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public </span><span style="background: white; color: #2b91af">IQueryable</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">Employee</span><span style="background: white; color: black">&gt; Employee()
        {
            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">_contextProvider.Context.Employees;
        }

        [</span><span style="background: white; color: #2b91af">HttpGet</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">Metadata()
        {
            </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">result = _contextProvider.Metadata();
            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">result;
        }
                        
        [</span><span style="background: white; color: #2b91af">HttpGet</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">ReSeed()
        {
            </span><span style="background: white; color: green">// Remove all records from the &quot;Employees&quot; table.
            </span><span style="background: white; color: black">_contextProvider.Context.Database.ExecuteSqlCommand(</span><span style="background: white; color: #a31515">&quot;truncate table Employees&quot;</span><span style="background: white; color: black">);

            </span><span style="background: white; color: green">// Run an &quot;Update-Database&quot; EF migrations command, this will update the database schema <br />            // to the latest state and run the Seed() method.
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">configuration = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">Research.UI.Web.Migrations.</span><span style="background: white; color: #2b91af">Configuration</span><span style="background: white; color: black">();
            configuration.ContextType = </span><span style="background: white; color: blue">typeof</span><span style="background: white; color: black">(</span><span style="background: white; color: #2b91af">ResearchDbContext</span><span style="background: white; color: black">);
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">migrator = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">DbMigrator</span><span style="background: white; color: black">(configuration);
            migrator.Update();
        }        

        [</span><span style="background: white; color: #2b91af">HttpPost</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public </span><span style="background: white; color: #2b91af">SaveResult </span><span style="background: white; color: black">SaveChanges(</span><span style="background: white; color: #2b91af">JObject </span><span style="background: white; color: black">saveBundle)
        {
            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">_contextProvider.SaveChanges(saveBundle);
        }
    }
}
</span></pre>

<p>&#160;</p>

<p>&#160;</p>

<p>For the complete code, see:</p>

<p><a title="https://github.com/roelvanlisdonk/Research/tree/master/Research/Research.UI.Web/Client/Features/AngularJS_and_Breeze/Part2" href="https://github.com/roelvanlisdonk/Research/tree/master/Research/Research.UI.Web/Client/Features/AngularJS_and_Breeze/Part2">https://github.com/roelvanlisdonk/Research/tree/master/Research/Research.UI.Web/Client/Features/AngularJS_and_Breeze/Part2</a></p>
---
ID: 3937
post_title: 'AngularJS and Breeze &ndash; A simple crud app &ndash; Part 1 &ndash;Automatic field data binding.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/07/10/how-to-loop-and-automatically-data-bind-breeze-entity-data-properties-fields-with-angularjs/
published: true
post_date: 2014-07-10 16:28:51
---
<p>&#160;</p>  <p>I wanted a really simple view in AngularJS, that would allow me to edit the data in a database table.</p>  <p>The view should show a grid containing a row for each record in the database.</p>  <p>Each record should show textboxes (html inputs) for all columns in the database, except the “Id” column.</p>  <p>In this way I could edit all data in a database table.</p>  <p>&#160;</p>  <p>Here’s the end result:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image15.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image_thumb15.png" width="580" height="338" /></a></p>  <p>&#160;</p>  <p>When the user clicks on the “save” button, the data is persisted to the database.</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image16.png" rel="lightbox"><img title="image" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border-top-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image_thumb16.png" width="580" height="340" /></a></p>  <p>&#160;</p>  <p>&#160;</p>  <p><strong>Breeze.js</strong></p>  <p>I decided to use Breeze.js for the data interaction.</p>  <p>The main trick I used to automatically data bind the Breeze.js entity data properties (fields) to the UI in AngularJS, is getting the names of the entity data properties (database table column names) from the metadata and then using a ng-repeat to loop over the table records and within this ng-repeat an other ng-repeat to loop over de Breeze entity data properties.</p>  <p>&#160;</p>  <p><strong>Getting table column names with Breeze (part of the client side code):</strong></p>  <p><span style="background: white; color: blue">var </span><span style="background: white; color: black">entityMetaData = manager.metadataStore.getEntityType(“Employee”);</span></p>  <p><span style="background: white; color: black">vm.entityFields = entityMetaData.dataProperties; </span></p>  <p><span style="background: white; color: black"></span></p>  <p>Automatically data bind, Breeze entity data properties (part of the client side code):</p>  <pre class="code"><p><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">tbody</span><span style="background: white; color: blue">&gt;
  &lt;</span><span style="background: white; color: maroon">tr </span><span style="background: white; color: red">ng-repeat</span><span style="background: white; color: blue">=&quot;entity in vm.entities&quot;&gt;
    &lt;</span><span style="background: white; color: maroon">td </span><span style="background: white; color: red">ng-repeat</span><span style="background: white; color: blue">='(key, prop) in vm.entityFields'&gt;<br /></span><span style="background: white; color: blue">      &lt;</span><span style="background: white; color: maroon">input </span><span style="background: white; color: red">ng-disabled</span><span style="background: white; color: blue">=&quot;{{vm.isReadOnlyField(prop.name)}}&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">='text' </span><span style="background: white; color: red">ng-model</span><span style="background: white; color: blue">='entity[prop.name]'&gt;<br />    &lt;/</span><span style="background: white; color: maroon">td</span><span style="background: white; color: blue">&gt;
  &lt;/</span><span style="background: white; color: maroon">tr</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">tbody</span><span style="background: white; color: blue">&gt;</span></p></pre>

<p><strong>Client side code</strong></p>

<pre class="code"><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">!DOCTYPE </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">html </span><span style="background: white; color: red">data-ng-app</span><span style="background: white; color: blue">=&quot;app&quot;&gt;
&lt;</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">title </span><span style="background: white; color: red">data-ng-bind</span><span style="background: white; color: blue">=&quot;title&quot;&gt;</span><span style="background: white; color: black">Research page</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">charset</span><span style="background: white; color: blue">=&quot;utf-8&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">http-equiv</span><span style="background: white; color: blue">=&quot;X-UA-Compatible&quot; </span><span style="background: white; color: red">content</span><span style="background: white; color: blue">=&quot;IE=edge, chrome=1&quot; /&gt;
    &lt;</span><span style="background: white; color: maroon">meta </span><span style="background: white; color: red">name</span><span style="background: white; color: blue">=&quot;viewport&quot; </span><span style="background: white; color: red">content</span><span style="background: white; color: blue">=&quot;width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1, <br />    user-scalable=no&quot; /&gt;

    </span><span style="background: white; color: #006400">&lt;!-- Libraries --&gt;
</span><span style="background: white; color: blue">    &lt;</span><span style="background: white; color: maroon">link </span><span style="background: white; color: red">rel</span><span style="background: white; color: blue">=&quot;stylesheet&quot; </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot; </span><span style="background: white; color: red">href</span><span style="background: white; color: blue">=&quot;../../Libraries/Toastr/toastr.min.css&quot; /&gt;
</span><span style="background: white; color: blue">
    </span><span style="background: white; color: #006400">&lt;!-- App --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;
        </span><span style="background: white; color: #006400">/* Resets */
        </span><span style="background: white; color: maroon">html</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">body</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">div</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">span</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">object</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">iframe</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">h1</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">h2</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">h3</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">h4</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">h5</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">h6</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">p</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">blockquote</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">pre</span><span style="background: white; color: black">,
        </span><span style="background: white; color: maroon">abbr</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">address</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">cite</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">code</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">del</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">dfn</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">em</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">img</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">ins</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">kbd</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">q</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">samp</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">small</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">strong</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">sub</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">sup</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">var</span><span style="background: white; color: black">,
        </span><span style="background: white; color: maroon">b</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">i</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">dl</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">dt</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">dd</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">ol</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">ul</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">li</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">fieldset</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">form</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">label</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">legend</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">table</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">caption</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">tbody</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">tfoot</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">thead</span><span style="background: white; color: black">, <br />        </span><span style="background: white; color: maroon">tr</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">th</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">td</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">article</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">aside</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">canvas</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">details</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">figcaption</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">figure</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">footer</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">header</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">hgroup</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">menu</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">nav</span><span style="background: white; color: black">,<br />        </span><span style="background: white; color: maroon">section</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">summary</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">time</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">mark</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">audio</span><span style="background: white; color: black">, </span><span style="background: white; color: maroon">video </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">border</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">0</span><span style="background: white; color: black">;              </span><span style="background: white; color: #006400">/* Prevent unnecessary white space. */
            </span><span style="background: white; color: red">-moz-box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">-webkit-box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">box-sizing</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">border-box</span><span style="background: white; color: black">; </span><span style="background: white; color: #006400">/* Padding, margin and borders are within the width and height of the element. */
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
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;spa-page&quot; </span><span style="background: white; color: red">data-ng-controller</span><span style="background: white; color: blue">=&quot;admin as vm&quot;&gt;
        &lt;</span><span style="background: white; color: maroon">a </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;spa-action-link&quot; </span><span style="background: white; color: red">ng-click</span><span style="background: white; color: blue">=&quot;vm.save()&quot;&gt;</span><span style="background: white; color: black">save</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">a</span><span style="background: white; color: blue">&gt;
        &lt;</span><span style="background: white; color: maroon">table</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">thead</span><span style="background: white; color: blue">&gt;
                &lt;</span><span style="background: white; color: maroon">tr</span><span style="background: white; color: blue">&gt;
                    &lt;</span><span style="background: white; color: maroon">th </span><span style="background: white; color: red">ng-repeat</span><span style="background: white; color: blue">='(key, prop) in vm.entityFields'&gt;</span><span style="background: white; color: black">{{ </span><span style="background: white; color: purple">prop.name </span><span style="background: white; color: black">}}</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">th</span><span style="background: white; color: blue">&gt;
                &lt;/</span><span style="background: white; color: maroon">tr</span><span style="background: white; color: blue">&gt;
            &lt;/</span><span style="background: white; color: maroon">thead</span><span style="background: white; color: blue">&gt;
            &lt;</span><span style="background: white; color: maroon">tbody</span><span style="background: white; color: blue">&gt;
                &lt;</span><span style="background: white; color: maroon">tr </span><span style="background: white; color: red">ng-repeat</span><span style="background: white; color: blue">=&quot;entity in vm.entities&quot;&gt;
                    &lt;</span><span style="background: white; color: maroon">td </span><span style="background: white; color: red">ng-repeat</span><span style="background: white; color: blue">='(key, prop) in vm.entityFields'&gt;<br />                      &lt;</span><span style="background: white; color: maroon">input </span><span style="background: white; color: red">ng-disabled</span><span style="background: white; color: blue">=&quot;{{vm.isReadOnlyField(prop.name)}}&quot;<br />                             </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">='text' <br />                             </span><span style="background: white; color: red">ng-model</span><span style="background: white; color: blue">='entity[prop.name]'&gt;<br />                    &lt;/</span><span style="background: white; color: maroon">td</span><span style="background: white; color: blue">&gt;
                &lt;/</span><span style="background: white; color: maroon">tr</span><span style="background: white; color: blue">&gt;
            &lt;/</span><span style="background: white; color: maroon">tbody</span><span style="background: white; color: blue">&gt;
        &lt;/</span><span style="background: white; color: maroon">table</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
    
    </span><span style="background: white; color: #006400">&lt;!-- Libraries --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;../../Libraries/Angular/angular.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;../../Libraries/Breeze/breeze.debug.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;../../Libraries/Breeze/breeze.angular.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;

    </span><span style="background: white; color: #006400">&lt;!-- Add toastr which needs jQuery (Breeze does not need jQuery) --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;../../Libraries/jQuery/jquery-2.1.1.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;../../Libraries/Toastr/toastr.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
</span><span style="background: white; color: #006400">    <br />    &lt;!-- Add breeze.savequeuing which needs Q (Breeze does not need Q)--&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;../../Libraries/Q/q.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot; </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;../../Libraries/Breeze/breeze.savequeuing.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    
    </span><span style="background: white; color: #006400">&lt;!-- App --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot;&gt;

        </span><span style="background: white; color: green">// Use namespaces to prevent pollution of the global namespace.
        </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">spa = spa || {};
        spa.controllers = spa.controllers || {};

        </span><span style="background: white; color: green">// Angular module [app].
        </span><span style="background: white; color: black">spa.app = (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
        {
            </span><span style="background: white; color: #a31515">'use strict'</span><span style="background: white; color: black">;

            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">app = angular.module(</span><span style="background: white; color: #a31515">'app'</span><span style="background: white; color: black">, [
                </span><span style="background: white; color: #a31515">'breeze.angular' </span><span style="background: white; color: green">// The breeze service module.
            </span><span style="background: white; color: black">]);
        })();

        </span><span style="background: white; color: green">// Angular controller [admin].
        </span><span style="background: white; color: black">spa.controllers.admin = (</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
        {
            </span><span style="background: white; color: #a31515">'use strict'</span><span style="background: white; color: black">;
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">controllerId = </span><span style="background: white; color: #a31515">'admin'</span><span style="background: white; color: black">;
            angular.module(</span><span style="background: white; color: #a31515">'app'</span><span style="background: white; color: black">).controller(controllerId, [</span><span style="background: white; color: #a31515">'breeze'</span><span style="background: white; color: black">, admin]);

            </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">admin(breeze)
            {
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">manager = </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">;
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">entityTypeName = </span><span style="background: white; color: #a31515">&quot;Employee&quot;</span><span style="background: white; color: black">;

                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">vm = </span><span style="background: white; color: blue">this</span><span style="background: white; color: black">;
                vm.entities = [];
                vm.entityFields = </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">;
                vm.isReadOnlyField = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(name)
                {
                    </span><span style="background: white; color: green">// Make 'id' fields read-only.
                    </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">(name === </span><span style="background: white; color: #a31515">'id'</span><span style="background: white; color: black">);
                };
                vm.save = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">()
                {
                    manager.saveChanges().then(showInfo).catch(showError);
                };
                
                </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">initialize()
                {
                    </span><span style="background: white; color: green">// Use camel case for entity properties.
                    </span><span style="background: white; color: black">breeze.NamingConvention.camelCase.setAsDefault();

                    </span><span style="background: white; color: green">// Configure and create EntityManager.<br />                    // The first breeze is part of the routing, second breeze is the name of the Web Api <br />                    // controller).
                    </span><span style="background: white; color: black">manager = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">breeze.EntityManager(</span><span style="background: white; color: #a31515">'/breeze/breeze'</span><span style="background: white; color: black">);
                    manager.enableSaveQueuing(</span><span style="background: white; color: blue">true</span><span style="background: white; color: black">);

                    </span><span style="background: white; color: green">// Get entities from the server.
                    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">query = </span><span style="background: white; color: blue">new </span><span style="background: white; color: black">breeze.EntityQuery().from(entityTypeName);
                    manager.executeQuery(query).then(handleRefresh).catch(showError);
                }

                </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">handleRefresh(data)
                {
                    </span><span style="background: white; color: green">// Get entity fields from metadata.
                    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">entityMetaData = manager.metadataStore.getEntityType(entityTypeName);
                    vm.entityFields = entityMetaData.dataProperties;

                    </span><span style="background: white; color: green">// Show the enties from the server.
                    </span><span style="background: white; color: black">vm.entities = data.results;
                }

                </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">showError(e)
                {
                    </span><span style="background: white; color: green">// Show xhr error.
                    </span><span style="background: white; color: black">toastr.error(e);
                }

                </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">showInfo()
                {
                    </span><span style="background: white; color: green">// Show info message.
                    </span><span style="background: white; color: black">toastr.info(entityTypeName + </span><span style="background: white; color: #a31515">&quot; saved!&quot;</span><span style="background: white; color: black">);
                }

                initialize();
            }
        })();
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
</span></pre>

<p>&#160;</p>

<p><strong>Sever side code</strong></p>

<p>&#160;</p>

<p><strong>Employee.cs</strong></p>

<pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">Research.UI.Web.Server.Model
{
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">Employee
    </span><span style="background: white; color: black">{
    </span><span style="background: white; color: black">    </span><span style="background: white; color: blue">public int </span><span style="background: white; color: black">Id { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
    </span><span style="background: white; color: black">    </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">FirstName { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
     </span><span style="background: white; color: black">   </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">LastName { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
      </span><span style="background: white; color: black">  </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">PhoneNumber { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
     </span><span style="background: white; color: black">}
}</span></pre>

<p><strong>ResearchDbContext.cs</strong></p>

<pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">Research.UI.Web.Server.Model
{
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Collections.Generic;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Data.Entity;

    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">ResearchDbContext </span><span style="background: white; color: black">: </span><span style="background: white; color: #2b91af">DbContext
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">public </span><span style="background: white; color: #2b91af">DbSet</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">Employee</span><span style="background: white; color: black">&gt; Employees { </span><span style="background: white; color: blue">get</span><span style="background: white; color: black">; </span><span style="background: white; color: blue">set</span><span style="background: white; color: black">; }
    </span><span style="background: white; color: black">}    
}</span></pre>

<p><strong>BreezeWebApiConfig.cs</strong></p>

<pre class="code"><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Web.Http;

[</span><span style="background: white; color: blue">assembly</span><span style="background: white; color: black">: WebActivator.</span><span style="background: white; color: #2b91af">PreApplicationStartMethod</span><span style="background: white; color: black">(
    </span><span style="background: white; color: blue">typeof</span><span style="background: white; color: black">(Research.UI.Web.App_Start.</span><span style="background: white; color: #2b91af">BreezeWebApiConfig</span><span style="background: white; color: black">), </span><span style="background: white; color: #a31515">&quot;RegisterBreezePreStart&quot;</span><span style="background: white; color: black">)]
</span><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">Research.UI.Web.App_Start {
  </span><span style="background: white; color: gray">///&lt;summary&gt;
  /// </span><span style="background: white; color: green">Inserts the Breeze Web API controller route at the front of all Web API routes
  </span><span style="background: white; color: gray">///&lt;/summary&gt;
  ///&lt;remarks&gt;
  /// </span><span style="background: white; color: green">This class is discovered and run during startup; see
  </span><span style="background: white; color: gray">/// </span><span style="background: white; color: green">http://blogs.msdn.com/b/davidebb/archive/2010/10/11/light-up-your-nupacks-with-startup-code-and-webactivator.aspx
  </span><span style="background: white; color: gray">///&lt;/remarks&gt;
  </span><span style="background: white; color: blue">public static class </span><span style="background: white; color: #2b91af">BreezeWebApiConfig </span><span style="background: white; color: black">{

    </span><span style="background: white; color: blue">public static void </span><span style="background: white; color: black">RegisterBreezePreStart() {
      </span><span style="background: white; color: #2b91af">GlobalConfiguration</span><span style="background: white; color: black">.Configuration.Routes.MapHttpRoute(
          name: </span><span style="background: white; color: #a31515">&quot;BreezeApi&quot;</span><span style="background: white; color: black">,
          routeTemplate: </span><span style="background: white; color: #a31515">&quot;breeze{controller}/{action}&quot;
      </span><span style="background: white; color: black">);
    }
  }
}</span></pre>

<p>&#160;</p>

<p><strong>BreezeController.cs</strong></p>

<pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">Research.UI.Web.Server.Controllers
{
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Breeze.ContextProvider;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Breeze.ContextProvider.EF6;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Breeze.WebApi2;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Newtonsoft.Json.Linq;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Research.UI.Web.Server.Components;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Research.UI.Web.Server.Model;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Linq;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Web.Http;

    [</span><span style="background: white; color: #2b91af">BreezeController</span><span style="background: white; color: black">]
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">BreezeController </span><span style="background: white; color: black">: </span><span style="background: white; color: #2b91af">ApiController
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">private readonly </span><span style="background: white; color: #2b91af">EFContextProvider</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">ResearchDbContext</span><span style="background: white; color: black">&gt; _contextProvider;
        </span><span style="background: white; color: blue">public </span><span style="background: white; color: black">BreezeController(): </span><span style="background: white; color: blue">this</span><span style="background: white; color: black">(</span><span style="background: white; color: blue">null</span><span style="background: white; color: black">)
        {
        }

        </span><span style="background: white; color: blue">public </span><span style="background: white; color: black">BreezeController(</span><span style="background: white; color: #2b91af">EFContextProvider</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">ResearchDbContext</span><span style="background: white; color: black">&gt; contextProvider</span><span style="background: white; color: black">)
        {
            _contextProvider = contextProvider ??  </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">EFContextProvider</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">ResearchDbContext</span><span style="background: white; color: black">&gt;();

         </span><span style="background: white; color: black">}</span><span style="background: white; color: black">

        [</span><span style="background: white; color: #2b91af">HttpGet</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public string </span><span style="background: white; color: black">Metadata()
        {
            </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">result = _contextProvider.Metadata();
            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">result;
        }

        [</span><span style="background: white; color: #2b91af">HttpGet</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public </span><span style="background: white; color: #2b91af">IQueryable</span><span style="background: white; color: black">&lt;</span><span style="background: white; color: #2b91af">Employee</span><span style="background: white; color: black">&gt; Employee()
        {
            
            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">_contextProvider.Context.Employees;
        }
    </span><span style="background: white; color: black">
        [</span><span style="background: white; color: #2b91af">HttpPost</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public </span><span style="background: white; color: #2b91af">SaveResult </span><span style="background: white; color: black">SaveChanges(</span><span style="background: white; color: #2b91af">JObject </span><span style="background: white; color: black">saveBundle)
        {
            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">_contextProvider.SaveChanges(saveBundle);
        }
    }
}
</span></pre>
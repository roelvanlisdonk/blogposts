---
ID: 3880
post_title: >
  Using Kendo UI switch with Font Awsome
  icons in a Kendo grid
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/07/02/using-kendo-ui-switch-with-font-awsome-icons-in-a-kendo-grid/
published: true
post_date: 2014-07-02 09:35:33
---
&nbsp;

If you want to use Kendo UI switch widgets with Font Awsome icons in a Kendo grid with MVVM binding, you can use the code below:

&nbsp;

<a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image.png" rel="lightbox"><img style="background-image: none; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border: 0px;" title="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/07/image_thumb.png" alt="image" width="580" height="138" border="0" /></a>

&nbsp;

<strong>Code</strong>
<pre class="code"><span style="background: white; color: blue;">&lt;</span><span style="background: white; color: maroon;">!DOCTYPE </span><span style="background: white; color: red;">html</span><span style="background: white; color: blue;">&gt;
&lt;</span><span style="background: white; color: maroon;">html</span><span style="background: white; color: blue;">&gt;
&lt;</span><span style="background: white; color: maroon;">head</span><span style="background: white; color: blue;">&gt;
    &lt;</span><span style="background: white; color: maroon;">title</span><span style="background: white; color: blue;">&gt;</span><span style="background: white; color: black;">Kendo element binding research page.</span><span style="background: white; color: blue;">&lt;/</span><span style="background: white; color: maroon;">title</span><span style="background: white; color: blue;">&gt;
    &lt;</span><span style="background: white; color: maroon;">link </span><span style="background: white; color: red;">rel</span><span style="background: white; color: blue;">="stylesheet" </span><span style="background: white; color: red;">type</span><span style="background: white; color: blue;">="text/css" </span><span style="background: white; color: red;">href</span><span style="background: white; color: blue;">="//cdn.kendostatic.com/2014.1.528/styles/kendo.common.min.css" /&gt;
    &lt;</span><span style="background: white; color: maroon;">link </span><span style="background: white; color: red;">rel</span><span style="background: white; color: blue;">="stylesheet" </span><span style="background: white; color: red;">type</span><span style="background: white; color: blue;">="text/css" </span><span style="background: white; color: red;">href</span><span style="background: white; color: blue;">="//cdn.kendostatic.com/2014.1.528/styles/kendo.rtl.min.css" /&gt;
    &lt;</span><span style="background: white; color: maroon;">link </span><span style="background: white; color: red;">rel</span><span style="background: white; color: blue;">="stylesheet" </span><span style="background: white; color: red;">type</span><span style="background: white; color: blue;">="text/css" </span><span style="background: white; color: red;">href</span><span style="background: white; color: blue;">="//cdn.kendostatic.com/2014.1.528/styles/kendo.metro.min.css" /&gt;
    &lt;</span><span style="background: white; color: maroon;">link </span><span style="background: white; color: red;">rel</span><span style="background: white; color: blue;">="stylesheet" </span><span style="background: white; color: red;">type</span><span style="background: white; color: blue;">="text/css" </span><span style="background: white; color: red;">href</span><span style="background: white; color: blue;">="//cdn.kendostatic.com/2014.1.528/styles/kendo.metro.mobile.min.css" /&gt;
    &lt;</span><span style="background: white; color: maroon;">link </span><span style="background: white; color: red;">rel</span><span style="background: white; color: blue;">="stylesheet" </span><span style="background: white; color: red;">type</span><span style="background: white; color: blue;">="text/css" </span><span style="background: white; color: red;">href</span><span style="background: white; color: blue;">="//netdna.bootstrapcdn.com/font-awesome/4.1.0/css/font-awesome.min.css"&gt;
    &lt;</span><span style="background: white; color: maroon;">style</span><span style="background: white; color: blue;">&gt;
        </span><span style="background: white; color: #006400;">/* Resets */
        </span><span style="background: white; color: maroon;">* </span><span style="background: white; color: black;">{
            </span><span style="background: white; color: red;">-moz-box-sizing</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">border-box</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">-webkit-box-sizing</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">border-box</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">box-sizing</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">border-box</span><span style="background: white; color: black;">; </span><span style="background: white; color: #006400;">/* Border boxing is used, so the padding, margin and borders are within the width and height of de element. */
            </span><span style="background: white; color: red;">color</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">rgb(112, 112, 112)</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">font-family</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">Arial</span><span style="background: white; color: black;">, </span><span style="background: white; color: blue;">Helvetica</span><span style="background: white; color: black;">, </span><span style="background: white; color: blue;">sans-serif</span><span style="background: white; color: black;">; </span><span style="background: white; color: #006400;">/* For know use default fonts used on google.com stackoverflow.com, telerik.com etc. */
            </span><span style="background: white; color: red;">font-size</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">13px</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">margin</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">0</span><span style="background: white; color: black;">; </span><span style="background: white; color: #006400;">/* Margin zero is used to prevent unnecessary white space. */
            </span><span style="background: white; color: red;">padding</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">0</span><span style="background: white; color: black;">; </span><span style="background: white; color: #006400;">/* Padding zero is used to prevent unnecessary white space. */
        </span><span style="background: white; color: black;">}

        </span><span style="background: white; color: maroon;">html</span><span style="background: white; color: black;">, </span><span style="background: white; color: maroon;">body </span><span style="background: white; color: black;">{
            </span><span style="background: white; color: red;">height</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">100%</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">max-height</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">100%</span><span style="background: white; color: black;">;
        }

        </span><span style="background: white; color: maroon;">body </span><span style="background: white; color: black;">{
            </span><span style="background: white; color: red;">padding</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">20px</span><span style="background: white; color: black;">;
        }

        </span><span style="background: white; color: maroon;">.info </span><span style="background: white; color: black;">{
            </span><span style="background: white; color: red;">border</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">1px solid rgb(128, 128, 128)</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">box-shadow</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">rgba(0, 0, 0, 0.298039) 0 2px 6px 0</span><span style="background: white; color: black;">, </span><span style="background: white; color: blue;">rgba(0, 0, 0, 0.2) 0 -3px 8px 0</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">padding</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">10px</span><span style="background: white; color: black;">;
        }

        </span><span style="background: white; color: maroon;">.addressRow </span><span style="background: white; color: black;">{
            </span><span style="background: white; color: red;">cursor</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">move</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">cursor</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">-webkit-grab</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">cursor</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">-moz-grab</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">height</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">10px</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">line-height</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">10px</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">padding</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">0</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">margin</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">0</span><span style="background: white; color: black;">;
        }

            </span><span style="background: white; color: maroon;">.addressRow input </span><span style="background: white; color: black;">{
                </span><span style="background: white; color: red;">font-family</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">FontAwesome</span><span style="background: white; color: black;">;
            }

        </span><span style="background: white; color: maroon;">#addressGrid tr &gt; td </span><span style="background: white; color: black;">{
            </span><span style="background: white; color: red;">height</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">1.6em</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">line-height</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">1.6em</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">padding</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">1px 4px 1px 4px</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">margin</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">0</span><span style="background: white; color: black;">;
        }

        </span><span style="background: white; color: maroon;">#addressGrid tr &gt; th </span><span style="background: white; color: black;">{
            </span><span style="background: white; color: red;">font-weight</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">bold</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">height</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">1.6em</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">line-height</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">1.6em</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">margin</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">0</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">padding</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">1px 4px 1px 4px</span><span style="background: white; color: black;">;
        }

        </span><span style="background: white; color: maroon;">#addressGrid tr &gt; td:first-child</span><span style="background: white; color: black;">, </span><span style="background: white; color: maroon;">#addressGrid tr &gt; th:first-child </span><span style="background: white; color: black;">{
            </span><span style="background: white; color: red;">width</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">56px</span><span style="background: white; color: black;">;
        }

        </span><span style="background: white; color: maroon;">#addressGrid tr:last-child td </span><span style="background: white; color: black;">{
            </span><span style="background: white; color: red;">padding-bottom</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">3px</span><span style="background: white; color: black;">;
        }

        </span><span style="background: white; color: maroon;">.km-switch </span><span style="background: white; color: black;">{
            </span><span style="background: white; color: red;">cursor</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">pointer</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">height</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">1.6em</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">line-height</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">1.6em</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">margin</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">0</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">padding</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">0</span><span style="background: white; color: black;">;
        }

        </span><span style="background: white; color: maroon;">#addressGrid tr &gt; td:first-child .km-switch-label-on</span><span style="background: white; color: black;">, </span><span style="background: white; color: maroon;">#addressGrid tr &gt; td:first-child .km-switch-label-off </span><span style="background: white; color: black;">{
            </span><span style="background: white; color: red;">font-family</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">FontAwesome</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">color</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">rgb(112, 112, 112)</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">height</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">1.6em</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: red;">line-height</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">1.6em</span><span style="background: white; color: black;">;
        }

        </span><span style="background: white; color: maroon;">#addressGrid tr &gt; td:first-child .km-switch-label-on:before </span><span style="background: white; color: black;">{
            </span><span style="background: white; color: red;">content</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">"\f023"</span><span style="background: white; color: black;">;
        }

        </span><span style="background: white; color: maroon;">#addressGrid tr &gt; td:first-child .km-switch-label-off:before </span><span style="background: white; color: black;">{
            </span><span style="background: white; color: red;">content</span><span style="background: white; color: black;">: </span><span style="background: white; color: blue;">"\f09c"</span><span style="background: white; color: black;">;
        }
    </span><span style="background: white; color: blue;">&lt;/</span><span style="background: white; color: maroon;">style</span><span style="background: white; color: blue;">&gt;

&lt;/</span><span style="background: white; color: maroon;">head</span><span style="background: white; color: blue;">&gt;
&lt;</span><span style="background: white; color: maroon;">body</span><span style="background: white; color: blue;">&gt;
    &lt;</span><span style="background: white; color: maroon;">div </span><span style="background: white; color: red;">id</span><span style="background: white; color: blue;">="view"&gt;
        &lt;</span><span style="background: white; color: maroon;">div </span><span style="background: white; color: red;">class</span><span style="background: white; color: blue;">="info"&gt;
            &lt;</span><span style="background: white; color: maroon;">script </span><span style="background: white; color: red;">id</span><span style="background: white; color: blue;">="addressRowTemplate" </span><span style="background: white; color: red;">type</span><span style="background: white; color: blue;">="text/x-kendo-tmpl"&gt;
                &lt;</span><span style="background: white; color: maroon;">tr </span><span style="background: white; color: red;">data-uid</span><span style="background: white; color: blue;">="#: uid#" </span><span style="background: white; color: red;">class</span><span style="background: white; color: blue;">="addressRow"&gt;
                    &lt;</span><span style="background: white; color: maroon;">td</span><span style="background: white; color: blue;">&gt;
                        &lt;</span><span style="background: white; color: maroon;">input </span><span style="background: white; color: red;">data-role</span><span style="background: white; color: blue;">="switch" </span><span style="background: white; color: red;">data-on-label</span><span style="background: white; color: blue;">="" </span><span style="background: white; color: red;">data-off-label</span><span style="background: white; color: blue;">="" </span><span style="background: white; color: red;">data-bind</span><span style="background: white; color: blue;">="checked: IsFixed"&gt;
                    &lt;/</span><span style="background: white; color: maroon;">td</span><span style="background: white; color: blue;">&gt;
                    &lt;</span><span style="background: white; color: maroon;">td</span><span style="background: white; color: blue;">&gt;
                        </span><span style="background: white; color: black;">#: Address#
                    </span><span style="background: white; color: blue;">&lt;/</span><span style="background: white; color: maroon;">td</span><span style="background: white; color: blue;">&gt;
                    &lt;</span><span style="background: white; color: maroon;">td</span><span style="background: white; color: blue;">&gt;
                        </span><span style="background: white; color: black;">#: Lat#
                    </span><span style="background: white; color: blue;">&lt;/</span><span style="background: white; color: maroon;">td</span><span style="background: white; color: blue;">&gt;
                    &lt;</span><span style="background: white; color: maroon;">td</span><span style="background: white; color: blue;">&gt;
                        </span><span style="background: white; color: black;">#: Long#
                    </span><span style="background: white; color: blue;">&lt;/</span><span style="background: white; color: maroon;">td</span><span style="background: white; color: blue;">&gt;
                    &lt;</span><span style="background: white; color: maroon;">td</span><span style="background: white; color: blue;">&gt;
                        &lt;</span><span style="background: white; color: maroon;">input </span><span style="background: white; color: red;">data-role</span><span style="background: white; color: blue;">="switch" </span><span style="background: white; color: red;">data-on-label</span><span style="background: white; color: blue;">="Y" </span><span style="background: white; color: red;">data-off-label</span><span style="background: white; color: blue;">="N" </span><span style="background: white; color: red;">data-bind</span><span style="background: white; color: blue;">="checked: IsFixed"&gt;
                    &lt;/</span><span style="background: white; color: maroon;">td</span><span style="background: white; color: blue;">&gt;
                &lt;/</span><span style="background: white; color: maroon;">tr</span><span style="background: white; color: blue;">&gt;
            &lt;/</span><span style="background: white; color: maroon;">script</span><span style="background: white; color: blue;">&gt;
            &lt;</span><span style="background: white; color: maroon;">div </span><span style="background: white; color: red;">id</span><span style="background: white; color: blue;">="addressGrid" </span><span style="background: white; color: red;">data-role</span><span style="background: white; color: blue;">="grid"
                 </span><span style="background: white; color: red;">data-row-template</span><span style="background: white; color: blue;">="addressRowTemplate"
                 </span><span style="background: white; color: red;">data-columns</span><span style="background: white; color: blue;">="[
                                    { 'field': 'IsFixed' },
                                    { 'field': 'Address' },
                                    { 'field': 'Lat' },
                                    { 'field': 'Long' },
                                    { 'field': 'Selected' }
                               ]"
                 </span><span style="background: white; color: red;">data-bind</span><span style="background: white; color: blue;">="source: addresses"&gt;&lt;/</span><span style="background: white; color: maroon;">div</span><span style="background: white; color: blue;">&gt;
        &lt;/</span><span style="background: white; color: maroon;">div</span><span style="background: white; color: blue;">&gt;
    &lt;/</span><span style="background: white; color: maroon;">div</span><span style="background: white; color: blue;">&gt;
    &lt;</span><span style="background: white; color: maroon;">script </span><span style="background: white; color: red;">type</span><span style="background: white; color: blue;">="text/javascript" </span><span style="background: white; color: red;">src</span><span style="background: white; color: blue;">="//code.jquery.com/jquery-1.9.1.min.js"&gt;&lt;/</span><span style="background: white; color: maroon;">script</span><span style="background: white; color: blue;">&gt;
    &lt;</span><span style="background: white; color: maroon;">script </span><span style="background: white; color: red;">type</span><span style="background: white; color: blue;">="text/javascript" </span><span style="background: white; color: red;">src</span><span style="background: white; color: blue;">="//cdn.kendostatic.com/2014.1.528/js/kendo.all.min.js"&gt;&lt;/</span><span style="background: white; color: maroon;">script</span><span style="background: white; color: blue;">&gt;</span><span style="background: white; color: blue;">
    &lt;</span><span style="background: white; color: maroon;">script </span><span style="background: white; color: red;">type</span><span style="background: white; color: blue;">="text/javascript"&gt;
        var </span><span style="background: white; color: black;">dataService = (</span><span style="background: white; color: blue;">function </span><span style="background: white; color: black;">()
        {
            </span><span style="background: white; color: #a31515;">"use strict"</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: blue;">var </span><span style="background: white; color: black;">self = {};

            self.getAddresses = </span><span style="background: white; color: blue;">function </span><span style="background: white; color: black;">()
            {
                </span><span style="background: white; color: blue;">var </span><span style="background: white; color: black;">data = </span><span style="background: white; color: blue;">new </span><span style="background: white; color: black;">kendo.data.ObservableArray(
                [
                    { Id: 1, Address: </span><span style="background: white; color: #a31515;">'Kerkweg 22'</span><span style="background: white; color: black;">,   Lat: </span><span style="background: white; color: #a31515;">'52.367443'</span><span style="background: white; color: black;">, Long: </span><span style="background: white; color: #a31515;">'4.865275'</span><span style="background: white; color: black;">, Selected: </span><span style="background: white; color: blue;">false</span><span style="background: white; color: black;">, IsFixed: </span><span style="background: white; color: blue;">false </span><span style="background: white; color: black;">},
                    { Id: 2, Address: </span><span style="background: white; color: #a31515;">'Peilstraat 3'</span><span style="background: white; color: black;">, Lat: </span><span style="background: white; color: #a31515;">'52.367967'</span><span style="background: white; color: black;">, Long: </span><span style="background: white; color: #a31515;">'4.866217'</span><span style="background: white; color: black;">, Selected: </span><span style="background: white; color: blue;">false</span><span style="background: white; color: black;">, IsFixed: </span><span style="background: white; color: blue;">true </span><span style="background: white; color: black;">},
                    { Id: 3, Address: </span><span style="background: white; color: #a31515;">'Bakkerloop 35'</span><span style="background: white; color: black;">, Lat: </span><span style="background: white; color: #a31515;">'52.367946'</span><span style="background: white; color: black;">, Long: </span><span style="background: white; color: #a31515;">'4.865482'</span><span style="background: white; color: black;">, Selected: </span><span style="background: white; color: blue;">false</span><span style="background: white; color: black;">, IsFixed: </span><span style="background: white; color: blue;">false </span><span style="background: white; color: black;">},
                    { Id: 4, Address: </span><span style="background: white; color: #a31515;">'Eikenlaan 1'</span><span style="background: white; color: black;">, Lat: </span><span style="background: white; color: #a31515;">'52.368237'</span><span style="background: white; color: black;">, Long: </span><span style="background: white; color: #a31515;">'4.866694'</span><span style="background: white; color: black;">, Selected: </span><span style="background: white; color: blue;">false</span><span style="background: white; color: black;">, IsFixed: </span><span style="background: white; color: blue;">true </span><span style="background: white; color: black;">}
                ]);

                </span><span style="background: white; color: green;">// Manual create a promise, so this function mimicks an Ajax call.
                </span><span style="background: white; color: blue;">var </span><span style="background: white; color: black;">dfd = </span><span style="background: white; color: blue;">new </span><span style="background: white; color: black;">$.Deferred();
                dfd.resolve(data);

                </span><span style="background: white; color: blue;">return </span><span style="background: white; color: black;">dfd.promise();
            };

            </span><span style="background: white; color: blue;">return </span><span style="background: white; color: black;">self;
        })(kendo);

        </span><span style="background: white; color: blue;">var </span><span style="background: white; color: black;">viewModel = </span><span style="background: white; color: blue;">new </span><span style="background: white; color: black;">kendo.observable({
            addresses: </span><span style="background: white; color: blue;">new </span><span style="background: white; color: black;">kendo.data.DataSource({ data: [] })
        });

        </span><span style="background: white; color: blue;">var </span><span style="background: white; color: black;">controller = (</span><span style="background: white; color: blue;">function </span><span style="background: white; color: black;">(dataService, viewModel)
        {
            </span><span style="background: white; color: #a31515;">"use strict"</span><span style="background: white; color: black;">;
            </span><span style="background: white; color: blue;">var </span><span style="background: white; color: black;">_dataService = dataService;            
            </span><span style="background: white; color: blue;">var </span><span style="background: white; color: black;">_vm = viewModel;
            </span><span style="background: white; color: blue;">var </span><span style="background: white; color: black;">self = {};
                        
            self.handleAdressesRefresh = </span><span style="background: white; color: blue;">function </span><span style="background: white; color: black;">(data)
            {
                _vm.set(</span><span style="background: white; color: #a31515;">"addresses"</span><span style="background: white; color: black;">, </span><span style="background: white; color: blue;">new </span><span style="background: white; color: black;">kendo.data.DataSource({ data: data }));
                kendo.bind($(</span><span style="background: white; color: #a31515;">".info"</span><span style="background: white; color: black;">), _vm);
            };

            self.show = </span><span style="background: white; color: blue;">function </span><span style="background: white; color: black;">()
            {
                $.when(_dataService.getAddresses())
                .then(self.handleAdressesRefresh);
            };

            </span><span style="background: white; color: blue;">return </span><span style="background: white; color: black;">self;
        })(dataService, viewModel);

        controller.show();
    </span><span style="background: white; color: blue;">&lt;/</span><span style="background: white; color: maroon;">script</span><span style="background: white; color: blue;">&gt;
&lt;/</span><span style="background: white; color: maroon;">body</span><span style="background: white; color: blue;">&gt;
&lt;/</span><span style="background: white; color: maroon;">html</span><span style="background: white; color: blue;">&gt;</span></pre>
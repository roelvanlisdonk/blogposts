---
ID: 770
post_title: >
  Prevent Internet Explorer, Google Chrome
  and Firefox from entering address bar
  after pressing TAB or SHIFT-TAB on the
  last or first element of the page
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/10/19/prevent-internet-explorer-google-chrome-and-firefox-from-entering-address-bar-after-pressing-tab-or-shift-tab-on-the-last-element-of-the-page/
published: true
post_date: 2009-10-19 20:42:32
---
<p>The normal behavior of a browser is to select the address bar after pressing tab on the last element of the page or shift tab on the first element on the page. Some customer who want to port a Windows application to a Web application want to copy the exact functionality of the Windows application (this is of course not a good idea) and want the tab order to stay in the web form. The following ASP .NET page shows how to make this functionality work on a web form, using CSS and JavaScript.&#160; <br />    <br />&#160;</p>  <pre class="code"><span style="background: #ffee62">&lt;%</span><span style="color: blue">@ </span><span style="color: #a31515">Page </span><span style="color: red">Language</span><span style="color: blue">=&quot;C#&quot; </span><span style="color: red">AutoEventWireup</span><span style="color: blue">=&quot;true&quot; </span><span style="color: red">CodeBehind</span><span style="color: blue">=&quot;Default.aspx.cs&quot; </span><span style="color: red">Inherits</span><span style="color: blue">=&quot;Rvl.HelperTools.Website._Default&quot; </span><span style="background: #ffee62">%&gt;

</span><span style="color: blue">&lt;!</span><span style="color: #a31515">DOCTYPE </span><span style="color: red">html PUBLIC </span><span style="color: blue">&quot;-//W3C//DTD XHTML 1.0 Transitional//EN&quot; &quot;http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd&quot;&gt;

&lt;</span><span style="color: #a31515">html </span><span style="color: red">xmlns</span><span style="color: blue">=&quot;http://www.w3.org/1999/xhtml&quot;&gt;
&lt;</span><span style="color: #a31515">head </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
    &lt;</span><span style="color: #a31515">title</span><span style="color: blue">&gt;</span>Test Page<span style="color: blue">&lt;/</span><span style="color: #a31515">title</span><span style="color: blue">&gt;

    &lt;</span><span style="color: #a31515">style </span><span style="color: red">type</span><span style="color: blue">=&quot;text/css&quot;&gt;
        </span><span style="color: #a31515">.FirstElementOnPage
        </span>{
            <span style="color: red">position</span>: <span style="color: blue">absolute</span>;
            <span style="color: red">top</span>: <span style="color: blue">-120px</span>;
            <span style="color: red">border</span>: <span style="color: blue">solid 1px white</span>;
            <span style="color: red">height</span>: <span style="color: blue">1px</span>;
            <span style="color: red">width</span>: <span style="color: blue">1px</span>;
        }
        <span style="color: #a31515">.LastElementOnPage
        </span>{
            <span style="color: red">position</span>: <span style="color: blue">absolute</span>;
            <span style="color: red">top</span>: <span style="color: blue">-100px</span>;
            <span style="color: red">border</span>: <span style="color: blue">solid 1px white</span>;
            <span style="color: red">height</span>: <span style="color: blue">1px</span>;
            <span style="color: red">width</span>: <span style="color: blue">1px</span>;
        }
        <span style="color: #a31515">.LastColumn
        </span>{
            <span style="color: red">border-left</span>: <span style="color: blue">solid 10px white</span>;
            <span style="color: red">text-align</span>: <span style="color: blue">left</span>;
            <span style="color: red">width</span>: <span style="color: blue">100%</span>;
        }
    <span style="color: blue">&lt;/</span><span style="color: #a31515">style</span><span style="color: blue">&gt;

    &lt;</span><span style="color: #a31515">script </span><span style="color: red">language</span><span style="color: blue">=&quot;javascript&quot; </span><span style="color: red">type</span><span style="color: blue">=&quot;text/javascript&quot;&gt;
        var </span>m_shiftKeyPressed = <span style="color: blue">false</span>;

        <span style="color: green">// This function focusses the given element. The funcion has a parameter event,
        // because the global event object is only defined in Internet Explorer.
        </span><span style="color: blue">function </span>SetFocusToElement(event, elementId, shiftKeyValue) {

            <span style="color: green">// Determine if Shift key is pressed.
            </span><span style="color: blue">if </span>(event.shiftKey) {
                <span style="color: green">// IE defines a global object event with a property shiftKey, use this property
                </span>shiftKeyIsPressed = event.shiftKey;
            }
            <span style="color: blue">else </span>{
                <span style="color: green">// Google chrome and firefox don't define a global event object and the event onblur event parameter does not contain a property shiftKey.
                // Use the determined value for m_shiftKeyPressed in the onKeyPressedDown event handler
                </span>shiftKeyIsPressed = m_shiftKeyPressed;
            }

            <span style="color: green">// Only focus when parameter shiftKeyValue == shiftKeyIsPressed
            </span><span style="color: blue">if </span>(shiftKeyIsPressed == shiftKeyValue) {

                <span style="color: green">// Find the element in DOM
                </span><span style="color: blue">var </span>elementToFocus = document.getElementById(elementId);

                <span style="color: green">// Must use setTimeout for google chrome, to set focus.
                </span><span style="color: blue">var </span>statementsToExcecute = <span style="color: #a31515">'document.getElementById(\'' </span>+ elementId + <span style="color: #a31515">'\').focus()'</span>;
                setTimeout(statementsToExcecute, 1);
            }

            <span style="color: green">// Must return true, for firefox to work
            </span><span style="color: blue">return true</span>;
        }
        <span style="color: blue">function </span>OnKeyUpFocusChange(event) {
            <span style="color: green">// Save if shift key is pressed, for use in onblur eventhandler.
            </span>m_shiftKeyPressed = event.shiftKey;
            <span style="color: blue">return true</span>;
        }
    <span style="color: blue">&lt;/</span><span style="color: #a31515">script</span><span style="color: blue">&gt;

&lt;/</span><span style="color: #a31515">head</span><span style="color: blue">&gt;
&lt;</span><span style="color: #a31515">body</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">form </span><span style="color: red">id</span><span style="color: blue">=&quot;mainForm&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot;&gt;
        &lt;</span><span style="color: #a31515">input </span><span style="color: red">id</span><span style="color: blue">=&quot;firstElementOnPage&quot; </span><span style="color: red">type</span><span style="color: blue">=&quot;text&quot; </span><span style="color: red">class</span><span style="color: blue">=&quot;FirstElementOnPage&quot; /&gt;
        &lt;</span><span style="color: #a31515">table</span><span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">tr</span><span style="color: blue">&gt;
                &lt;</span><span style="color: #a31515">td</span><span style="color: blue">&gt;&lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Label </span><span style="color: red">ID</span><span style="color: blue">=&quot;customerLabel&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">Text</span><span style="color: blue">=&quot;Customer&quot;&gt;&lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Label</span><span style="color: blue">&gt;&lt;/</span><span style="color: #a31515">td</span><span style="color: blue">&gt;
                &lt;</span><span style="color: #a31515">td </span><span style="color: red">class</span><span style="color: blue">=&quot;LastColumn&quot;&gt;&lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">TextBox </span><span style="color: red">ID</span><span style="color: blue">=&quot;customerTextBox&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">Text</span><span style="color: blue">=&quot;Microsoft&quot; </span><span style="color: red">onkeydown</span><span style="color: blue">=&quot;OnKeyUpFocusChange(event);&quot;
                </span><span style="color: red">onblur</span><span style="color: blue">=&quot;SetFocusToElement(event, 'submitButton', true);&quot;&gt;&lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">TextBox</span><span style="color: blue">&gt;&lt;/</span><span style="color: #a31515">td</span><span style="color: blue">&gt;
            &lt;/</span><span style="color: #a31515">tr</span><span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">tr</span><span style="color: blue">&gt;
                &lt;</span><span style="color: #a31515">td</span><span style="color: blue">&gt;&lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Label </span><span style="color: red">ID</span><span style="color: blue">=&quot;cityLabel&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">Text</span><span style="color: blue">=&quot;City&quot;&gt;&lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Label</span><span style="color: blue">&gt;&lt;/</span><span style="color: #a31515">td</span><span style="color: blue">&gt;
                &lt;</span><span style="color: #a31515">td </span><span style="color: red">class</span><span style="color: blue">=&quot;LastColumn&quot;&gt;&lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">TextBox </span><span style="color: red">ID</span><span style="color: blue">=&quot;cityTextBox&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">Text</span><span style="color: blue">=&quot;Redmond&quot;&gt;&lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">TextBox</span><span style="color: blue">&gt;&lt;/</span><span style="color: #a31515">td</span><span style="color: blue">&gt;
            &lt;/</span><span style="color: #a31515">tr</span><span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">tr</span><span style="color: blue">&gt;
                &lt;</span><span style="color: #a31515">td</span><span style="color: blue">&gt;&lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Label </span><span style="color: red">ID</span><span style="color: blue">=&quot;supplierLabel&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">Text</span><span style="color: blue">=&quot;Supplier&quot;&gt;&lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Label</span><span style="color: blue">&gt;&lt;/</span><span style="color: #a31515">td</span><span style="color: blue">&gt;
                &lt;</span><span style="color: #a31515">td </span><span style="color: red">class</span><span style="color: blue">=&quot;LastColumn&quot;&gt;&lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">TextBox </span><span style="color: red">ID</span><span style="color: blue">=&quot;supplierTextBox&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">Text</span><span style="color: blue">=&quot;IBM&quot;&gt;&lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">TextBox</span><span style="color: blue">&gt;&lt;/</span><span style="color: #a31515">td</span><span style="color: blue">&gt;
            &lt;/</span><span style="color: #a31515">tr</span><span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">tr</span><span style="color: blue">&gt;
                &lt;</span><span style="color: #a31515">td</span><span style="color: blue">&gt;&lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Label </span><span style="color: red">ID</span><span style="color: blue">=&quot;productsLabel&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">Text</span><span style="color: blue">=&quot;Products&quot;&gt;&lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">Label</span><span style="color: blue">&gt;&lt;/</span><span style="color: #a31515">td</span><span style="color: blue">&gt;
                &lt;</span><span style="color: #a31515">td </span><span style="color: red">class</span><span style="color: blue">=&quot;LastColumn&quot;&gt;&lt;</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">TextBox </span><span style="color: red">ID</span><span style="color: blue">=&quot;productsTextBox&quot; </span><span style="color: red">runat</span><span style="color: blue">=&quot;server&quot; </span><span style="color: red">Text</span><span style="color: blue">=&quot;Windows&quot;&gt;&lt;/</span><span style="color: #a31515">asp</span><span style="color: blue">:</span><span style="color: #a31515">TextBox</span><span style="color: blue">&gt;&lt;/</span><span style="color: #a31515">td</span><span style="color: blue">&gt;
            &lt;/</span><span style="color: #a31515">tr</span><span style="color: blue">&gt;
        &lt;/</span><span style="color: #a31515">table</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">input </span><span style="color: red">id</span><span style="color: blue">=&quot;submitButton&quot; </span><span style="color: red">type</span><span style="color: blue">=&quot;button&quot; </span><span style="color: red">value</span><span style="color: blue">=&quot;Submit&quot; </span><span style="color: red">onblur</span><span style="color: blue">=&quot;SetFocusToElement(event, 'customerTextBox', false);&quot; /&gt;
        &lt;</span><span style="color: #a31515">input </span><span style="color: red">id</span><span style="color: blue">=&quot;lastElementOnPage&quot; </span><span style="color: red">type</span><span style="color: blue">=&quot;text&quot; </span><span style="color: red">class</span><span style="color: blue">=&quot;LastElementOnPage&quot;  /&gt;
    &lt;/</span><span style="color: #a31515">form</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">body</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">html</span><span style="color: blue">&gt;</span></pre>
<a href="http://11011.net/software/vspaste"></a><a href="http://11011.net/software/vspaste"></a>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/10/image7.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/10/image_thumb7.png" width="445" height="262" /></a> </p>

<p>After pressing the tab key on when the Submit button has focus, the customer textbox will be focused.</p>
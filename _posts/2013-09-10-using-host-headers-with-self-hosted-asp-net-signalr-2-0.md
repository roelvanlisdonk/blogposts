---
ID: 3421
post_title: >
  Using host headers with self hosted
  ASP.NET SignalR 2.0
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/09/10/using-host-headers-with-self-hosted-asp-net-signalr-2-0/
published: true
post_date: 2013-09-10 16:40:14
---
<p>If you want to use host headers in development with self hosted ASP .NET SignalR 2.0, you can add the hostheader to your hosts file, found in C:\Windows\System32\Drivers\etc</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image15.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/09/image_thumb15.png" width="580" height="414" /></a></p>  <p>&#160;</p>  <p>Then use the following adjusted client and server from the tutorial at <a href="http://www.asp.net/signalr/overview/getting-started/tutorial-signalr-self-host">http://www.asp.net/signalr/overview/getting-started/tutorial-signalr-self-host</a>: </p>  <p>&#160;</p>  <p><strong>Server</strong></p>  <pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">SignalRSelfHost
{
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Microsoft.AspNet.SignalR;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Microsoft.Owin.Hosting;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Owin;

    </span><span style="background: white; color: blue">class </span><span style="background: white; color: #2b91af">Program
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">static void </span><span style="background: white; color: black">Main(</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">[] args)
        {
            </span><span style="background: white; color: green">// This will *ONLY* bind to localhost, if you want to bind to all addresses
            // use http://*:8080 to bind to all addresses. 
            // See http://msdn.microsoft.com/en-us/library/system.net.httplistener.aspx 
            // for more information.
            
            //string url = &quot;http://localhost:8080&quot;;
            </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">url = </span><span style="background: white; color: #a31515">&quot;http://rlitest.nl&quot;</span><span style="background: white; color: black">;

            </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: #2b91af">WebApp</span><span style="background: white; color: black">.Start&lt;</span><span style="background: white; color: #2b91af">Startup</span><span style="background: white; color: black">&gt;(url))
            {
                </span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.WriteLine(</span><span style="background: white; color: #a31515">&quot;Server running on {0}&quot;</span><span style="background: white; color: black">, url);
                </span><span style="background: white; color: #2b91af">Console</span><span style="background: white; color: black">.ReadLine();
            }
        }
    }
    </span><span style="background: white; color: blue">class </span><span style="background: white; color: #2b91af">Startup
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Configuration(</span><span style="background: white; color: #2b91af">IAppBuilder </span><span style="background: white; color: black">app)
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">config = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">HubConfiguration</span><span style="background: white; color: black">();
            config.EnableJSONP = </span><span style="background: white; color: blue">true</span><span style="background: white; color: black">;
            app.MapSignalR(config);
        }
    }
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">MyHub </span><span style="background: white; color: black">: </span><span style="background: white; color: #2b91af">Hub
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Send(</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">name, </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">message)
        {
            Clients.All.addMessage(name, message);
        }
    }
}
</span></pre>



<p><strong>Client</strong></p>

<pre class="code"><span style="background: white; color: blue">&lt;!</span><span style="background: white; color: maroon">DOCTYPE </span><span style="background: white; color: red">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;</span><span style="background: white; color: black">SignalR Simple Chat</span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">title</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">style </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/css&quot;&gt;
        </span><span style="background: white; color: maroon">.container </span><span style="background: white; color: black">{
            </span><span style="background: white; color: red">background-color</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">#99CCFF</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">border</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">thick solid #808080</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">padding</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">20px</span><span style="background: white; color: black">;
            </span><span style="background: white; color: red">margin</span><span style="background: white; color: black">: </span><span style="background: white; color: blue">20px</span><span style="background: white; color: black">;
        }
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">style</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">head</span><span style="background: white; color: blue">&gt;
&lt;</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: maroon">div </span><span style="background: white; color: red">class</span><span style="background: white; color: blue">=&quot;container&quot;&gt;
        &lt;</span><span style="background: white; color: maroon">input </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text&quot; </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;message&quot; /&gt;
        &lt;</span><span style="background: white; color: maroon">input </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;button&quot; </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;sendmessage&quot; </span><span style="background: white; color: red">value</span><span style="background: white; color: blue">=&quot;Send&quot; /&gt;
        &lt;</span><span style="background: white; color: maroon">input </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;hidden&quot; </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;displayname&quot; /&gt;
        &lt;</span><span style="background: white; color: maroon">ul </span><span style="background: white; color: red">id</span><span style="background: white; color: blue">=&quot;discussion&quot;&gt;&lt;/</span><span style="background: white; color: maroon">ul</span><span style="background: white; color: blue">&gt;
    &lt;/</span><span style="background: white; color: maroon">div</span><span style="background: white; color: blue">&gt;
    </span><span style="background: white; color: #006400">&lt;!--Script references. --&gt;
    &lt;!--Reference the jQuery library. --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;Scripts/jquery-1.6.4.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    </span><span style="background: white; color: #006400">&lt;!--Reference the SignalR library. --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;Scripts/jquery.signalR-2.0.0-rc1.min.js&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    </span><span style="background: white; color: #006400">&lt;!--Reference the autogenerated SignalR hub script. --&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">src</span><span style="background: white; color: blue">=&quot;http://rlitest.nl/signalr/hubs&quot;&gt;&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
    </span><span style="background: white; color: #006400">&lt;!--Add script to update the page and send messages.--&gt;
    </span><span style="background: white; color: blue">&lt;</span><span style="background: white; color: maroon">script </span><span style="background: white; color: red">type</span><span style="background: white; color: blue">=&quot;text/javascript&quot;&gt;
        </span><span style="background: white; color: black">$(</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
            </span><span style="background: white; color: green">//Set the hubs URL for the connection

            //$.connection.hub.url = &quot;http://localhost:8080/signalr&quot;;
            </span><span style="background: white; color: black">$.connection.hub.url = </span><span style="background: white; color: #a31515">&quot;http://rlitest.nl/signalr&quot;</span><span style="background: white; color: black">;

            </span><span style="background: white; color: green">// Declare a proxy to reference the hub.
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">chat = $.connection.myHub;

            </span><span style="background: white; color: green">// Create a function that the hub can call to broadcast messages.
            </span><span style="background: white; color: black">chat.client.addMessage = </span><span style="background: white; color: blue">function </span><span style="background: white; color: black">(name, message) {
                </span><span style="background: white; color: green">// Html encode display name and message.
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">encodedName = $(</span><span style="background: white; color: #a31515">'&lt;div /&gt;'</span><span style="background: white; color: black">).text(name).html();
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">encodedMsg = $(</span><span style="background: white; color: #a31515">'&lt;div /&gt;'</span><span style="background: white; color: black">).text(message).html();
                </span><span style="background: white; color: green">// Add the message to the page.
                </span><span style="background: white; color: black">$(</span><span style="background: white; color: #a31515">'#discussion'</span><span style="background: white; color: black">).append(</span><span style="background: white; color: #a31515">'&lt;li&gt;&lt;strong&gt;' </span><span style="background: white; color: black">+ encodedName
                    + </span><span style="background: white; color: #a31515">'&lt;/strong&gt;:&amp;nbsp;&amp;nbsp;' </span><span style="background: white; color: black">+ encodedMsg + </span><span style="background: white; color: #a31515">'&lt;/li&gt;'</span><span style="background: white; color: black">);
            };
            </span><span style="background: white; color: green">// Get the user name and store it to prepend to messages.
            </span><span style="background: white; color: black">$(</span><span style="background: white; color: #a31515">'#displayname'</span><span style="background: white; color: black">).val(prompt(</span><span style="background: white; color: #a31515">'Enter your name:'</span><span style="background: white; color: black">, </span><span style="background: white; color: #a31515">''</span><span style="background: white; color: black">));
            </span><span style="background: white; color: green">// Set initial focus to message input box.
            </span><span style="background: white; color: black">$(</span><span style="background: white; color: #a31515">'#message'</span><span style="background: white; color: black">).focus();
            </span><span style="background: white; color: green">// Start the connection.
            </span><span style="background: white; color: black">$.connection.hub.start({ jsonp: </span><span style="background: white; color: blue">true </span><span style="background: white; color: black">}).done(</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
                $(</span><span style="background: white; color: #a31515">'#sendmessage'</span><span style="background: white; color: black">).click(</span><span style="background: white; color: blue">function </span><span style="background: white; color: black">() {
                    </span><span style="background: white; color: green">// Call the Send method on the hub.
                    </span><span style="background: white; color: black">chat.server.send($(</span><span style="background: white; color: #a31515">'#displayname'</span><span style="background: white; color: black">).val(), $(</span><span style="background: white; color: #a31515">'#message'</span><span style="background: white; color: black">).val());
                    </span><span style="background: white; color: green">// Clear text box and reset focus for next comment.
                    </span><span style="background: white; color: black">$(</span><span style="background: white; color: #a31515">'#message'</span><span style="background: white; color: black">).val(</span><span style="background: white; color: #a31515">''</span><span style="background: white; color: black">).focus();
                });
            });
        });
    </span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: maroon">script</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">body</span><span style="background: white; color: blue">&gt;
&lt;/</span><span style="background: white; color: maroon">html</span><span style="background: white; color: blue">&gt;</span></pre>
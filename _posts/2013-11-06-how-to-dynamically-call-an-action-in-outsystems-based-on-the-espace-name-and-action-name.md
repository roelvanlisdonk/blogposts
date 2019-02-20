---
ID: 3545
post_title: >
  How to dynamically call an action in
  Outsystems, based on the eSpace name and
  Action name.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/11/06/how-to-dynamically-call-an-action-in-outsystems-based-on-the-espace-name-and-action-name/
published: true
post_date: 2013-11-06 22:25:07
---
<p>This post describes how to call an action in Outsystems, based on a given eSpace name and action name.</p>  <p>&#160;</p>  <p>Lets says you want the user to select a action name from a dropdownlist and execute this action, then you can create a big switch statement to call the actions supplied in the dropdownlist, but if you don’t want to change this switch statement each time a new action is added to the list, then you have to create an Outsystems actions and write some C# code, to dynamically execute the action based on a given eSpace name and action name.</p>  <p>&#160;</p>  <p><strong>Extension</strong></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/11/image3.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/11/image_thumb3.png" width="580" height="378" /></a></p>  <p>&#160;</p>  <p><strong>Visual Studio</strong></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/11/image4.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/11/image_thumb4.png" width="244" height="187" /></a></p>  <p>&#160;</p>  <p><strong>C# code</strong></p>   <pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">OutSystems.NssDynamicExtension {

</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Collections;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Data;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">OutSystems.HubEdition.RuntimePlatform;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">GotDotNet.ApplicationBlocks;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Text;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Linq;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Reflection;

</span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">CssDynamicExtension</span><span style="background: white; color: black">: </span><span style="background: white; color: #2b91af">IssDynamicExtension </span><span style="background: white; color: black">{

</span><span style="background: white; color: gray">/// &lt;summary&gt;
/// 
/// &lt;/summary&gt;
/// &lt;param name=&quot;ssresult&quot;&gt;&lt;/param&gt;
/// &lt;param name=&quot;sseSpaceName&quot;&gt;&lt;/param&gt;
/// &lt;param name=&quot;ssactionName&quot;&gt;&lt;/param&gt;
</span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">MssInvokeAction(</span><span style="background: white; color: blue">out string </span><span style="background: white; color: black">ssresult, </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">sseSpaceName, </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">ssactionName) {
    ssresult = </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Empty;
    </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">messages = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">StringBuilder</span><span style="background: white; color: black">(</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Empty);

    </span><span style="background: white; color: blue">try
    </span><span style="background: white; color: black">{

        </span><span style="background: white; color: green">// Get all assemblies in current AppDomain.
        </span><span style="background: white; color: #2b91af">AppDomain </span><span style="background: white; color: black">currentDomain = </span><span style="background: white; color: #2b91af">AppDomain</span><span style="background: white; color: black">.CurrentDomain;
        </span><span style="background: white; color: #2b91af">Assembly</span><span style="background: white; color: black">[] assemblies = currentDomain.GetAssemblies();

        </span><span style="background: white; color: green">// Log all assemblynames.
        </span><span style="background: white; color: black">assemblies.ToList()
            .OrderBy(x =&gt; x.FullName).ToList()
            .ForEach(x =&gt; { messages.AppendLine(x.GetName().Name); });

        </span><span style="background: white; color: green">// Get eSpace assembly.
        </span><span style="background: white; color: #2b91af">Assembly </span><span style="background: white; color: black">eSpaceAssemlby = assemblies.ToList()
                    .First(x =&gt; x.GetName().Name.Equals(sseSpaceName, </span><span style="background: white; color: #2b91af">StringComparison</span><span style="background: white; color: black">.InvariantCultureIgnoreCase));

        </span><span style="background: white; color: green">// Get assembly that contians the &quot;HeContext&quot; type.
        </span><span style="background: white; color: #2b91af">Assembly </span><span style="background: white; color: black">runtimePlatform = assemblies.ToList()
                .First(x =&gt; x.GetName().Name.Equals(</span><span style="background: white; color: #a31515">&quot;OutSystems.HubEdition.RuntimePlatform&quot;</span><span style="background: white; color: black">));

        </span><span style="background: white; color: green">// Get the type that contains all actions from an eSpace.
        </span><span style="background: white; color: #2b91af">Type </span><span style="background: white; color: black">actionsType = eSpaceAssemlby.GetType(</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">&quot;ss{0}.Actions&quot;</span><span style="background: white; color: black">, sseSpaceName));

        </span><span style="background: white; color: green">// Get &quot;HeContext&quot; type (curent HttpContext object).
        </span><span style="background: white; color: #2b91af">Type </span><span style="background: white; color: black">contextType = runtimePlatform.GetType(</span><span style="background: white; color: #a31515">&quot;OutSystems.HubEdition.RuntimePlatform.HeContext&quot;</span><span style="background: white; color: black">);

        </span><span style="background: white; color: green">// Create an instance of the &quot;HeContext&quot; type.
        </span><span style="background: white; color: blue">object </span><span style="background: white; color: black">contextInstance = </span><span style="background: white; color: #2b91af">Activator</span><span style="background: white; color: black">.CreateInstance(contextType);

        </span><span style="background: white; color: green">// Invoke the given action and supply as first parameter the &quot;HeContext&quot; (curent HttpContext) object.
        </span><span style="background: white; color: black">actionsType.InvokeMember(</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">&quot;Action{0}&quot;</span><span style="background: white; color: black">, ssactionName), 
                                </span><span style="background: white; color: #2b91af">BindingFlags</span><span style="background: white; color: black">.InvokeMethod | </span><span style="background: white; color: #2b91af">BindingFlags</span><span style="background: white; color: black">.Static | </span><span style="background: white; color: #2b91af">BindingFlags</span><span style="background: white; color: black">.Public, 
                                </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">new object</span><span style="background: white; color: black">[] { contextInstance });
    }
    </span><span style="background: white; color: blue">catch </span><span style="background: white; color: black">(</span><span style="background: white; color: #2b91af">Exception </span><span style="background: white; color: black">ex)
    {
        messages.AppendLine(ex.ToString());
    }

    ssresult = messages.ToString();
} </span><span style="background: white; color: green">// MssInvokeAction

</span><span style="background: white; color: black">} </span><span style="background: white; color: green">// CssDynamicExtension

</span><span style="background: white; color: black">} </span><span style="background: white; color: green">// OutSystems.NssDynamicExtension

</span></pre>


<p>&#160;</p>

<p><strong>Use the action in Outsystems</strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/11/image5.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/11/image_thumb5.png" width="580" height="306" /></a></p>

<p>&#160;</p>

<p><strong>Result</strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/11/image6.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/11/image_thumb6.png" width="418" height="473" /></a></p>

<p>&#160;</p>

<p>The action that was dynamically invoked, inserted a record in the database and I could see this record was created, so everything worked just fine.</p>

<p>&#160;</p>

<p>So instead of:</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/11/image7.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/11/image_thumb7.png" width="461" height="481" /></a></p>

<p>&#160;</p>

<p>My code now looks like this:</p>

<p>&#160;</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/11/image8.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/11/image_thumb8.png" width="294" height="462" /></a></p>

<p>&#160;</p>

<p>&#160;</p>

<p>Sometimes, reflection is your friend <img class="wlEmoticon wlEmoticon-smile" style="border-top-style: none; border-left-style: none; border-bottom-style: none; border-right-style: none" alt="Smile" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/11/wlEmoticon-smile.png" />.</p>
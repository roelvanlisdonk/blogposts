---
ID: 2303
post_title: 'How to deserialize an object containing collections from an App.config or Web.config in .NET 4.0 and C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/12/15/how-to-deserialize-an-object-containing-collections-from-an-app-config-or-web-config/
published: true
post_date: 2011-12-15 11:00:54
---
<p>Let says you want to store your application settings in an App.config or Web.config file and these settings should contain collections of settings, then use can use the following code to deserialize an object containing these settings from an App.config or Web.config. By using deserialization the object can contain any type that’s serializable.</p>  <p>&#160;</p>  <p><strong>The App.config</strong></p>  <pre class="code"><span style="color: blue">&lt;?</span><span style="color: #a31515">xml </span><span style="color: red">version</span><span style="color: blue">=</span>&quot;<span style="color: blue">1.0</span>&quot; <span style="color: red">encoding</span><span style="color: blue">=</span>&quot;<span style="color: blue">utf-8</span>&quot; <span style="color: blue">?&gt;
&lt;</span><span style="color: #a31515">configuration</span><span style="color: blue">&gt;
  &lt;</span><span style="color: #a31515">configSections</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">section </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">ApplicationSettings</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">Rvl.NewCode.Test.BC.ApplicationSettings, Rvl.NewCode.Test</span>&quot; <span style="color: blue">/&gt;
  &lt;/</span><span style="color: #a31515">configSections</span><span style="color: blue">&gt;
  &lt;</span><span style="color: #a31515">ApplicationSettings</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">Id</span><span style="color: blue">&gt;</span>12<span style="color: blue">&lt;/</span><span style="color: #a31515">Id</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">CarTypes</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">string</span><span style="color: blue">&gt;</span>Audi<span style="color: blue">&lt;/</span><span style="color: #a31515">string</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">string</span><span style="color: blue">&gt;</span>BMW<span style="color: blue">&lt;/</span><span style="color: #a31515">string</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">string</span><span style="color: blue">&gt;</span>Mercedes<span style="color: blue">&lt;/</span><span style="color: #a31515">string</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">CarTypes</span><span style="color: blue">&gt;
  &lt;/</span><span style="color: #a31515">ApplicationSettings</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">configuration</span><span style="color: blue">&gt;
</span></pre>


<p>&#160;</p>

<p><strong>The code to deserialize the object from the App.config file</strong></p>

<pre class="code"><span style="color: #2b91af">ApplicationSettings </span>settings = <span style="color: blue">new </span><span style="color: #2b91af">ApplicationSettings</span>();
settings.InitializeFromAppConfig();</pre>


<p>After running this code the settings object, contains the data:</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/12/image13.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/12/image_thumb13.png" width="580" height="191" /></a></p>

<p>&#160;</p>

<p><strong>The ApplicationSettings class</strong></p>

<pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Configuration;
<span style="color: blue">using </span>System.IO;
<span style="color: blue">using </span>System.Text;
<span style="color: blue">using </span>System.Xml;
<span style="color: blue">using </span>System.Xml.Serialization;
<span style="color: blue">namespace </span>Rvl.NewCode.Test.BC
{
    <span style="color: blue">public class </span><span style="color: #2b91af">ApplicationSettings </span>: <span style="color: #2b91af">IConfigurationSectionHandler
    </span>{
        <span style="color: blue">public int </span>Id { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
        <span style="color: blue">public </span><span style="color: #2b91af">List</span>&lt;<span style="color: blue">string</span>&gt; CarTypes { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Creates a configuration section handler.
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;parent&quot;&gt;</span><span style="color: green">Parent object.</span><span style="color: gray">&lt;/param&gt;
        /// &lt;param name=&quot;configContext&quot;&gt;</span><span style="color: green">Configuration context object.</span><span style="color: gray">&lt;/param&gt;
        /// &lt;param name=&quot;section&quot;&gt;</span><span style="color: green">Section XML node.</span><span style="color: gray">&lt;/param&gt;
        /// &lt;returns&gt;
        /// </span><span style="color: green">The created section handler object.
        </span><span style="color: gray">/// &lt;/returns&gt;
        </span><span style="color: blue">public object </span>Create(<span style="color: blue">object </span>parent, <span style="color: blue">object </span>configContext, System.Xml.<span style="color: #2b91af">XmlNode </span>section)
        {
            <span style="color: blue">return </span>section;
        }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Initialize this object from app config.
        </span><span style="color: gray">/// &lt;/summary&gt;
        </span><span style="color: blue">public void </span>InitializeFromAppConfig()
        {
            <span style="color: #2b91af">XmlElement </span>settingsXmlElement       = GetXmlElementFromAppConfig();
            <span style="color: #2b91af">ApplicationSettings </span>settings    = DeserializeFromXmlElement(settingsXmlElement);
            CopyDataToCurrentObject(settings);
        }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Gets the XML element from app config.
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;returns&gt;
        /// </span><span style="color: green">The found xml element.
        </span><span style="color: gray">/// &lt;/returns&gt;
        </span><span style="color: blue">private </span><span style="color: #2b91af">XmlElement </span>GetXmlElementFromAppConfig()
        {
            <span style="color: blue">string </span>tagName = <span style="color: blue">this</span>.GetType().Name;
            <span style="color: #2b91af">XmlElement </span>sectionElement = <span style="color: #2b91af">ConfigurationManager</span>.GetSection(tagName) <span style="color: blue">as </span><span style="color: #2b91af">XmlElement</span>;
            <span style="color: blue">if </span>(sectionElement == <span style="color: blue">null</span>)
            {
                <span style="color: blue">throw new </span><span style="color: #2b91af">ApplicationException</span>(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;Could not find section [{0}] in the App.config file.&quot;</span>, tagName));
            }
            <span style="color: blue">return </span>sectionElement;
        }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Convert the given XML element to a ScheduleServiceSettings object.
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;sectionElement&quot;&gt;</span><span style="color: green">The XML element containing the information to create a ScheduleServiceSettings object.</span><span style="color: gray">&lt;/param&gt;
        /// &lt;returns&gt;</span><span style="color: green">A ScheduleServiceSettings object</span><span style="color: gray">&lt;/returns&gt;
        </span><span style="color: blue">private </span><span style="color: #2b91af">ApplicationSettings </span>DeserializeFromXmlElement(<span style="color: #2b91af">XmlElement </span>sectionElement)
        {
            <span style="color: #2b91af">ApplicationSettings </span>settings = <span style="color: blue">null</span>;
            <span style="color: blue">using </span>(<span style="color: #2b91af">StringReader </span>reader = <span style="color: blue">new </span><span style="color: #2b91af">StringReader</span>(sectionElement.OuterXml))
            {
                <span style="color: #2b91af">XmlSerializer </span>xs    = <span style="color: blue">new </span><span style="color: #2b91af">XmlSerializer</span>(<span style="color: blue">typeof</span>(<span style="color: #2b91af">ApplicationSettings</span>));
                settings            = xs.Deserialize(reader) <span style="color: blue">as </span><span style="color: #2b91af">ApplicationSettings</span>;
            }
            <span style="color: blue">return </span>settings;
        }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Copy the data found in the ScheduleServiceSettings object to the current object
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;settings&quot;&gt;&lt;/param&gt;
        </span><span style="color: blue">private void </span>CopyDataToCurrentObject(<span style="color: #2b91af">ApplicationSettings </span>settings)
        {
            Id = settings.Id;
            CarTypes = settings.CarTypes;
        }
    }
}</pre>
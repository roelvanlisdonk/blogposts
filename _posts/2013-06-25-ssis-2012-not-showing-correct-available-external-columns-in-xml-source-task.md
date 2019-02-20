---
ID: 3282
post_title: >
  SSIS 2012 not showing correct Available
  External Columns in Xml Source Task.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/06/25/ssis-2012-not-showing-correct-available-external-columns-in-xml-source-task/
published: true
post_date: 2013-06-25 16:14:06
---
<p>&nbsp;</p> <p>The "ORDER" type in the following XML document will not be shown in the available external columns dialog in SSIS 2012.</p> <p>&lt;?xml version="1.0" encoding="utf-8"?&gt;<br>&lt;ORDER&gt;<br>&nbsp; &lt;ID&gt;1&lt;/ID&gt;<br>&nbsp; &lt;ORDERLINE&gt;<br>&nbsp;&nbsp;&nbsp; &lt;ID&gt;1&lt;/ID&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;PRODUCTNAME&gt;Test1&lt;/PRODUCTNAME&gt;<br>&nbsp; &lt;/ORDERLINE&gt;<br>&nbsp; &lt;ORDERLINE&gt;<br>&nbsp;&nbsp;&nbsp; &lt;ID&gt;2&lt;/ID&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;PRODUCTNAME&gt;Test2&lt;/PRODUCTNAME&gt;<br>&nbsp; &lt;/ORDERLINE&gt;<br>&lt;/ORDER&gt;<br></p> <p>&nbsp;</p> <p><strong>Result</strong></p> <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image16.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image_thumb16.png" width="580" height="534"></a></p> <p>&nbsp;</p> <p>If you want the ORDER type to show up, add a root element to the xml document:</p> <p>&nbsp;</p> <p>&lt;?xml version="1.0" encoding="utf-8"?&gt;<br>&lt;ROOT&gt;<br>&nbsp;&nbsp;&nbsp; &lt;ORDER&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;ID&gt;1&lt;/ID&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;ORDERLINE&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;ID&gt;1&lt;/ID&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;PRODUCTNAME&gt;Test1&lt;/PRODUCTNAME&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;/ORDERLINE&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;ORDERLINE&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;ID&gt;2&lt;/ID&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;PRODUCTNAME&gt;Test2&lt;/PRODUCTNAME&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;/ORDERLINE&gt;<br>&nbsp;&nbsp;&nbsp; &lt;/ORDER&gt;<br>&lt;/ROOT&gt;</p> <p>&nbsp;</p> <p>Now you will see both ORDER and ORDERLINE show up:</p> <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image17.png" rel="lightbox"><img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 5px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2013/06/image_thumb17.png" width="580" height="386"></a></p> <p>&nbsp;</p> <p>To add a root node to an XML document in SSIS you can use the following script code:</p><pre class="code"><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Main()
 {
 </span><span style="background: white; color: blue">try
 </span><span style="background: white; color: black">{
 </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">selectedXmlFile = Dts.Variables[</span><span style="background: white; color: #a31515">@"User::SelectedXmlFile"</span><span style="background: white; color: black">].Value.ToString();
 </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">AlteredXmlFile = (</span><span style="background: white; color: #2b91af">String</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">"{0}x"</span><span style="background: white; color: black">, selectedXmlFile));
 Dts.Variables[</span><span style="background: white; color: #a31515">@"User::AlteredXmlFile"</span><span style="background: white; color: black">].Value = selectedXmlFile;

 </span><span style="background: white; color: #2b91af">XmlDocument </span><span style="background: white; color: black">oldDoc = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">XmlDocument</span><span style="background: white; color: black">();
 oldDoc.Load(selectedXmlFile);

 </span><span style="background: white; color: #2b91af">XmlDocument </span><span style="background: white; color: black">newDoc = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">XmlDocument</span><span style="background: white; color: black">();
 </span><span style="background: white; color: #2b91af">XmlElement </span><span style="background: white; color: black">root = newDoc.CreateElement(</span><span style="background: white; color: #a31515">"ROOT"</span><span style="background: white; color: black">);
 newDoc.InsertAfter(root, </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">);

 </span><span style="background: white; color: #2b91af">XmlNode </span><span style="background: white; color: black">content = newDoc.ImportNode(oldDoc.ChildNodes[2], </span><span style="background: white; color: blue">true</span><span style="background: white; color: black">);
 root.AppendChild(content);

 newDoc.Save(AlteredXmlFile);

 Dts.TaskResult = (</span><span style="background: white; color: blue">int</span><span style="background: white; color: black">)</span><span style="background: white; color: #2b91af">ScriptResults</span><span style="background: white; color: black">.Success;
 }
 </span><span style="background: white; color: blue">catch </span><span style="background: white; color: black">(</span><span style="background: white; color: #2b91af">Exception </span><span style="background: white; color: black">ex)
 {
 Dts.Variables[</span><span style="background: white; color: #a31515">@"User::LogMessage"</span><span style="background: white; color: black">].Value = ex.ToString();
 Dts.TaskResult = (</span><span style="background: white; color: blue">int</span><span style="background: white; color: black">)</span><span style="background: white; color: #2b91af">ScriptResults</span><span style="background: white; color: black">.Failure;
 }

 }
</pre></span>
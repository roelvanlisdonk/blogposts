---
ID: 2644
post_title: 'How to validate a XML file against a XSD file, including the referenced schemas by the XSD file in C#.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/03/30/how-to-validate-a-xml-file-against-a-xsd-file-including-the-referenced-schemas-by-the-xsd-file-in-c/
published: true
post_date: 2012-03-30 13:45:58
---
<p>If you want to validate an XML file against a XSD file and use the XSD schemas referenced by the XSD file in the validation, you can use the following C# code:</p>   <p>&#160;</p>   <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.IO;
<span style="color: blue">using </span>System.Xml;
<span style="color: blue">using </span>System.Xml.Schema;
<span style="color: blue">using </span>Microsoft.VisualStudio.TestTools.UnitTesting;

<span style="color: blue">namespace </span>Research.Rli
{
<span style="color: gray">/// &lt;summary&gt;
/// </span><span style="color: green">Tests in this class are only used to analyse and research code.
</span><span style="color: gray">/// </span><span style="color: green">It is not intended to contain real integration tests.
</span><span style="color: gray">/// &lt;/summary&gt;
</span>[<span style="color: #2b91af">TestClass</span>]
<span style="color: blue">public class </span><span style="color: #2b91af">RliResearchTester
</span>{
<span style="color: blue">public </span>RliResearchTester()
{
}

<span style="color: gray">/// &lt;summary&gt;
/// </span><span style="color: green">Test xml validation against a XSD file.
</span><span style="color: gray">/// &lt;/summary&gt;
</span>[<span style="color: #2b91af">TestMethod</span>]
<span style="color: blue">public void </span>ValidateXmlTest()
{
    ValidateXml(<span style="color: #a31515">@&quot;C:\Data\Input.xml&quot;</span>, <span style="color: #a31515">@&quot;C:\Data\ValidationSchema.xsd&quot;</span>);
}
<span style="color: gray">/// &lt;summary&gt;
/// </span><span style="color: green">Validates a xml file (found at the given xmlFilePath) to a XSD file (found at the given xsdFilePath).
</span><span style="color: gray">/// &lt;/summary&gt;
/// &lt;param name=&quot;xmlFilePath&quot;&gt;</span><span style="color: green">The xml file to validate.</span><span style="color: gray">&lt;/param&gt;
/// &lt;param name=&quot;xsdFilePath&quot;&gt;</span><span style="color: green">The xsd file used in the validation.</span><span style="color: gray">&lt;/param&gt;
/// &lt;exception cref=&quot;ArgumentNullException&quot;&gt;
/// </span><span style="color: green">Throws an ArgumentNullException, when xmlFilePath is null, empty or contains only white spaces.
</span><span style="color: gray">/// &lt;/exception&gt;
/// &lt;exception cref=&quot;ArgumentNullException&quot;&gt;
/// </span><span style="color: green">Throws an ArgumentNullException, when xsdFilePath is null, empty or contains only white spaces.
</span><span style="color: gray">/// &lt;/exception&gt;
/// &lt;exception cref=&quot;ArgumentException&quot;&gt;</span><span style="color: green">Throws an ArgumentException, when xmlFilePath does not exist.</span><span style="color: gray">&lt;/exception&gt;
/// &lt;exception cref=&quot;ArgumentException&quot;&gt;</span><span style="color: green">Throws an ArgumentException, when xsdFilePath does not exist.</span><span style="color: gray">&lt;/exception&gt;
/// &lt;remarks&gt;
/// </span><span style="color: green">- Includes schemas referenced by the given xsd file (recursively).
</span><span style="color: gray">/// &lt;/remarks&gt;
</span><span style="color: blue">public void </span>ValidateXml(<span style="color: blue">string </span>xmlFilePath, <span style="color: blue">string </span>xsdFilePath)
{
    <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrWhiteSpace(xmlFilePath)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;xmlFilePath&quot;</span>); }
    <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrWhiteSpace(xsdFilePath)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;xsdFilePath&quot;</span>); }
    <span style="color: blue">if </span>(!<span style="color: #2b91af">File</span>.Exists(xmlFilePath))
    {
        <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentException</span>(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;File [{0}] not found.&quot;</span>, xmlFilePath));
    }
    <span style="color: blue">if </span>(!<span style="color: #2b91af">File</span>.Exists(xsdFilePath))
    {
        <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentException</span>(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;File [{0}] not found.&quot;</span>, xsdFilePath));
    }

    <span style="color: blue">var </span>schemas = <span style="color: blue">new </span><span style="color: #2b91af">XmlSchemaSet</span>();

    <span style="color: green">// Use the target namespace specified in the XSD file. 
    </span>schemas.Add(<span style="color: blue">null</span>, xsdFilePath);

    <span style="color: blue">var </span>readerSettings = <span style="color: blue">new </span><span style="color: #2b91af">XmlReaderSettings</span>();

    <span style="color: green">// Validate the xml file to an XSD file not an DTD or XDR.
    </span>readerSettings.ValidationType = <span style="color: #2b91af">ValidationType</span>.Schema;

    <span style="color: green">// Include schemas referenced by the given xsd file (recursively) in the validation proces.
    </span>readerSettings.ValidationFlags |= <span style="color: #2b91af">XmlSchemaValidationFlags</span>.ProcessSchemaLocation;

    <span style="color: green">// Warnings will fire the ValidationEventHandler function.
    </span>readerSettings.ValidationFlags |= <span style="color: #2b91af">XmlSchemaValidationFlags</span>.ReportValidationWarnings;
    readerSettings.Schemas.Add(schemas);

    <span style="color: green">// The function [ValidationEventHandler] will be used to handle all validation errors / warnings.
    </span>readerSettings.ValidationEventHandler += ValidationEventHandler;

    <span style="color: blue">using </span>(<span style="color: blue">var </span>xmlReader = <span style="color: #2b91af">XmlReader</span>.Create(xmlFilePath, readerSettings))
    {
        <span style="color: blue">while </span>(xmlReader.Read()) { }    <span style="color: green">// Validate XML file.
    </span>}
}
<span style="color: gray">/// &lt;summary&gt;
/// </span><span style="color: green">This event will fire on every XML validation error / warning.
</span><span style="color: gray">/// &lt;/summary&gt;
/// &lt;param name=&quot;sender&quot;&gt;&lt;/param&gt;
/// &lt;param name=&quot;args&quot;&gt;&lt;/param&gt;
</span><span style="color: blue">public void </span>ValidationEventHandler(<span style="color: blue">object </span>sender, <span style="color: #2b91af">ValidationEventArgs </span>args)
{
    <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;&quot;</span>,
        <span style="color: blue">new object</span>[] { args.Exception, args.Exception.LineNumber, args.Exception.LinePosition }));
}
}
}</pre>
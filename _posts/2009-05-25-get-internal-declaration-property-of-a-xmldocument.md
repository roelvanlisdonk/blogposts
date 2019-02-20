---
ID: 465
post_title: >
  Get internal Declaration property of a
  XmlDocument
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/25/get-internal-declaration-property-of-a-xmldocument/
published: true
post_date: 2009-05-25 09:03:46
---
<p></p>  <div class="padten">   <div class="ms-inputuserfield padfive seventyp">     <div>       <div class="ExternalClass98B11DDD84B44A098CE4732C72CB21D0">         <pre class="code"><span style="color: gray">The XmlDocument class contains a internal property Declaration of type XmlDeclaration. </span></pre>

        <pre class="code"><span style="color: gray">To use the information in this object use the following code:</span></pre>

        <pre class="code"><span style="color: gray"></span>&#160;</pre>

        <pre class="code"><span style="color: blue">public string </span>GetXmlDocumentDeclarationText()
        {
            <span style="color: blue">string </span>xmlText = <span style="color: #a31515">@&quot;&lt;?xml version=&quot;&quot;1.0&quot;&quot; encoding=&quot;&quot;utf-8&quot;&quot;?&gt;
&lt;RootNode&gt;
    &lt;SubNode&gt;
    &lt;/SubNode&gt;
&lt;/RootNode&gt;
&quot;</span>;
            System.Xml.<span style="color: #2b91af">XmlDocument </span>doc = <span style="color: blue">new </span>System.Xml.<span style="color: #2b91af">XmlDocument</span>();
            doc.LoadXml(xmlText);
            System.Xml.<span style="color: #2b91af">XmlDeclaration </span>dec = (System.Xml.<span style="color: #2b91af">XmlDeclaration</span>)<span style="color: blue">this</span>.GetPrivateProperty(doc, <span style="color: #a31515">&quot;Declaration&quot;</span>);
            <span style="color: blue">return </span>dec.OuterXml.Trim();
        }
        <span style="color: blue">public object </span>GetPrivateField(<span style="color: blue">object </span>target, <span style="color: blue">string </span>field)
        {
            System.Reflection.<span style="color: #2b91af">FieldInfo </span>fi = target.GetType().GetField(field, </pre>

        <blockquote>
          <pre class="code"><span style="color: #2b91af">BindingFlags</span>.FlattenHierarchy | <span style="color: #2b91af">BindingFlags</span>.Instance | <span style="color: #2b91af">BindingFlags</span>.NonPublic | <span style="color: #2b91af">BindingFlags</span>.Public | <span style="color: #2b91af">BindingFlags</span>.Static);
            <span style="color: blue">return </span>fi.GetValue(target);
        }</pre>
        </blockquote>
      </div>
    </div>
  </div>
</div>
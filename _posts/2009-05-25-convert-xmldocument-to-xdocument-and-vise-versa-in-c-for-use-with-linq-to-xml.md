---
ID: 472
post_title: 'Convert XmlDocument to XDocument and vise versa in C# (for use with Linq to XML)'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/25/convert-xmldocument-to-xdocument-and-vise-versa-in-c-for-use-with-linq-to-xml/
published: true
post_date: 2009-05-25 12:54:15
---
<div class="padten">   <div class="ms-inputuserfield padfive seventyp">     <div>       <div class="ExternalClass6A20077B82194F66BB2BE3B17AC23B3F">         <p>If you have an XmlDocument and you want't to query it with linq, you first have to convert the XmlDocument to an XDocument:           <br /></p>          <blockquote>           <pre class="code"><span style="color: green">// Convert XmlDocument to XDocument
</span><span style="color: #2b91af">XmlDocument </span>xmlDocument = <span style="color: blue">new </span><span style="color: #2b91af">XmlDocument</span>();
xmlDocument.Load(<span style="color: #a31515">@&quot;C:\Temp\Test.xml&quot;</span>);
<span style="color: #2b91af">XDocument </span>xDocument = <span style="color: #2b91af">XDocument</span>.Parse(xmlDocument.OuterXml);<br /><br /><br /></pre>

          <pre class="code"><span style="color: green">// Convert XDocument to XmlDocument
</span>xmlDocument.LoadXml(xDocument.ToString());</pre>
        </blockquote>
      </div>
    </div>
  </div>
</div>
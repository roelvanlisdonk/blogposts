---
ID: 2084
post_title: >
  Solving Unable to generate a temporary
  class error CS2001 en CS2008
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/06/08/solving-unable-to-generate-a-temporary-class-error-cs2001-en-cs2008/
published: true
post_date: 2011-06-08 20:48:37
---
<p>&#160;</p>  <h1>Error</h1>  <p>&#160;</p>  <pre>System.InvalidOperationException: Unable to generate a temporary class (result=1).
error CS2001: Source file &amp;#39;C:\Windows\TEMP\beo4ycyh.0.cs&amp;#39; could not be found
error CS2008: No inputs specified

   at System.Xml.Serialization.Compiler.Compile(Assembly parent, String ns, XmlSerializerCompilerParameters xmlParameters, Evidence evidence)
   at System.Xml.Serialization.TempAssembly.GenerateAssembly(XmlMapping[] xmlMappings, Type[] types, String defaultNamespace, Evidence evidence, XmlSerializerCompilerParameters parameters, Assembly assembly, Hashtable assemblies)
   at System.Xml.Serialization.TempAssembly..ctor(XmlMapping[] xmlMappings, Type[] types, String defaultNamespace, String location, Evidence evidence)
   at System.Xml.Serialization.XmlSerializer.FromMappings(XmlMapping[] mappings, Type type)
   at System.Web.Services.Protocols.XmlReturn.GetInitializers(LogicalMethodInfo[] methodInfos)
   at System.Web.Services.Protocols.HttpServerType..ctor(Type type)
   at System.Web.Services.Protocols.HttpServerProtocol.Initialize()
   at System.Web.Services.Protocols.ServerProtocolFactory.Create(Type type, HttpContext context, HttpRequest request, HttpResponse response, Boolean&amp; abortProcessing)</pre>

<p>&#160;</p>

<h1>Solution</h1>

<p>After adding the application pool service account to the local administrators group, this error was resolved.</p>

<p>We are now looking into a real solution <img style="border-bottom-style: none; border-left-style: none; border-top-style: none; border-right-style: none" class="wlEmoticon wlEmoticon-winkingsmile" alt="Winking smile" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/06/wlEmoticon-winkingsmile.png" /></p>
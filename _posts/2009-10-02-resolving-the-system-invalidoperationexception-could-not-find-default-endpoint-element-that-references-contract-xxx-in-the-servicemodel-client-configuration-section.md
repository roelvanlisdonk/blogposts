---
ID: 735
post_title: 'Resolving the System.InvalidOperationException : Could not find default endpoint element that references contract &#8216;xxx&#8217; in the ServiceModel client configuration section'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/10/02/resolving-the-system-invalidoperationexception-could-not-find-default-endpoint-element-that-references-contract-xxx-in-the-servicemodel-client-configuration-section/
published: true
post_date: 2009-10-02 16:20:05
---
<p>After renaming a WCF service reference in Microsoft Visual Studio, you can get the error:   <br /></p>  <p>System.InvalidOperationException : Could not find default endpoint element that references contract 'ImportServiceReference.IImportService' in the ServiceModel client configuration section. This might be because no configuration file was found for your application, or because no endpoint element matching this contract could be found in the client element.   <br />&#160;&#160;&#160; at System.ServiceModel.Description.ConfigLoader.LoadChannelBehaviors(ServiceEndpoint serviceEndpoint, String configurationName)    <br />&#160;&#160;&#160; at System.ServiceModel.ChannelFactory.InitializeEndpoint(String configurationName, EndpointAddress address)    <br />&#160;&#160;&#160; at System.ServiceModel.ChannelFactory`1..ctor(String endpointConfigurationName, EndpointAddress remoteAddress)    <br />&#160;&#160;&#160; at System.ServiceModel.ChannelFactory`1..ctor(String endpointConfigurationName)    <br />&#160;&#160;&#160; at System.ServiceModel.EndpointTrait`1.CreateSimplexFactory()    <br />&#160;&#160;&#160; at System.ServiceModel.EndpointTrait`1.CreateChannelFactory()    <br />&#160;&#160;&#160; at System.ServiceModel.ClientBase`1.CreateChannelFactoryRef(EndpointTrait`1 endpointTrait)    <br />&#160;&#160;&#160; at System.ServiceModel.ClientBase`1.InitializeChannelFactoryRef()    <br />&#160;&#160;&#160; at System.ServiceModel.ClientBase`1..ctor()</p>  <p>   <br />Make sure the name in the contract attribute of the endpoint is the same as you’re Microsoft Visual Studio Service Reference name</p>  <pre class="code"><span style="color: blue">&lt;</span><span style="color: #a31515">endpoint </span><span style="color: red">address</span><span style="color: blue">=</span>&quot;<span style="color: blue"><a href="http://localhost/ImportService/ImportService.svc&quot;">http://localhost/ImportService/ImportService.svc</span>&quot;
</a>        <span style="color: red">binding</span><span style="color: blue">=</span>&quot;<span style="color: blue">wsHttpBinding</span>&quot; <span style="color: red">bindingConfiguration</span><span style="color: blue">=</span>&quot;<span style="color: blue">WSHttpBinding_IImportService</span>&quot;
        <span style="color: red">contract</span><span style="color: blue">=</span>&quot;<span style="color: blue"><strong><font size="4">ImportServiceReference</font></strong>.IImportService</span>&quot; <span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">WSHttpBinding_IImportService</span>&quot;<span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">identity</span><span style="color: blue">&gt;
          &lt;</span><span style="color: #a31515">dns </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">localhost</span>&quot; <span style="color: blue">/&gt;
        &lt;/</span><span style="color: #a31515">identity</span><span style="color: blue">&gt;
      &lt;/</span><span style="color: #a31515">endpoint</span><span style="color: blue">&gt;</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>Must be the same as:
  <br />

  <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/10/image2.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/10/image_thumb2.png" width="222" height="39" /></a></p>
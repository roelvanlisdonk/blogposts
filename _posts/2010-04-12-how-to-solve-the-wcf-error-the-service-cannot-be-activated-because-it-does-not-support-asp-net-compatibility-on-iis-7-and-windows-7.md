---
ID: 1232
post_title: 'How to solve: The WCF error &ldquo;The service cannot be activated because it does not support ASP.NET compatibility&rdquo; on IIS 7 and Windows 7'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/04/12/how-to-solve-the-wcf-error-the-service-cannot-be-activated-because-it-does-not-support-asp-net-compatibility-on-iis-7-and-windows-7/
published: true
post_date: 2010-04-12 21:38:32
---
<p>&#160;</p>  <p>On IIS 7 and Windows 7, I got an error (see error below), when debugging mine WCF service. </p>  <p>Turned out I had to set [AspNetCompatibilityRequirements(RequirementsMode = AspNetCompatibilityRequirementsMode.Allowed)] on mine service:   <br />    <br /></p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Runtime.Serialization;
<span style="color: blue">using </span>System.ServiceModel;
<span style="color: blue">using </span>System.ServiceModel.Web;
<span style="color: blue">using </span>System.Text;
<span style="color: blue">using </span>System.ServiceModel.Activation;

<span style="color: blue">namespace </span>WcfService1
{
<span style="color: green">    </span>[<span style="color: #2b91af">AspNetCompatibilityRequirements</span>(RequirementsMode = <span style="color: #2b91af">AspNetCompatibilityRequirementsMode</span>.Allowed)]
    <span style="color: blue">public class </span><span style="color: #2b91af">Service1 </span>: <span style="color: #2b91af">IService1
    </span>{
        <span style="color: blue">public string </span>GetData(<span style="color: blue">int </span>value)
        {
            <span style="color: blue">return string</span>.Format(<span style="color: #a31515">&quot;You entered: {0}&quot;</span>, value);
        }

        <span style="color: blue">public </span><span style="color: #2b91af">CompositeType </span>GetDataUsingDataContract(<span style="color: #2b91af">CompositeType </span>composite)
        {
            <span style="color: blue">if </span>(composite == <span style="color: blue">null</span>)
            {
                <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;composite&quot;</span>);
            }
            <span style="color: blue">if </span>(composite.BoolValue)
            {
                composite.StringValue += <span style="color: #a31515">&quot;Suffix&quot;</span>;
            }
            <span style="color: blue">return </span>composite;
        }
    }
}</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p>&#160;</p>

<h3>Server Error in '/WcfService1' Application. 
  <hr size="1" width="100%" /></h3>

<h4><i>The service cannot be activated because it does not support ASP.NET compatibility. ASP.NET compatibility is enabled for this application. Turn off ASP.NET compatibility mode in the web.config or add the AspNetCompatibilityRequirements attribute to the service type with RequirementsMode setting as 'Allowed' or 'Required'.</i></h4>
<b>Description: </b>An unhandled exception occurred during the execution of the current web request. Please review the stack trace for more information about the error and where it originated in the code. 

<br /><b>Exception Details: </b>System.InvalidOperationException: The service cannot be activated because it does not support ASP.NET compatibility. ASP.NET compatibility is enabled for this application. Turn off ASP.NET compatibility mode in the web.config or add the AspNetCompatibilityRequirements attribute to the service type with RequirementsMode setting as 'Allowed' or 'Required'.

<br /><b>Source Error:</b>

<p><code>An unhandled exception was generated during the execution of the current web request. Information regarding the origin and location of the exception can be identified using the exception stack trace below.</code></p>

<p><b>Stack Trace:</b></p>

<p><code></code>

  <pre>[InvalidOperationException: The service cannot be activated because it does not support ASP.NET compatibility. ASP.NET compatibility is enabled for this application. Turn off ASP.NET compatibility mode in the web.config or add the AspNetCompatibilityRequirements attribute to the service type with RequirementsMode setting as 'Allowed' or 'Required'.]
   System.ServiceModel.Activation.HostedAspNetEnvironment.ValidateCompatibilityRequirements(AspNetCompatibilityRequirementsMode compatibilityMode) +183896
   System.ServiceModel.Description.DispatcherBuilder.ValidateDescription(ServiceDescription description, ServiceHostBase serviceHost) +441
   System.ServiceModel.Description.DispatcherBuilder.InitializeServiceHost(ServiceDescription description, ServiceHostBase serviceHost) +306
   System.ServiceModel.ServiceHostBase.InitializeRuntime() +82
   System.ServiceModel.Channels.CommunicationObject.Open(TimeSpan timeout) +612
   System.ServiceModel.HostingManager.ActivateService(String normalizedVirtualPath) +287
   System.ServiceModel.HostingManager.EnsureServiceAvailable(String normalizedVirtualPath) +1132

[ServiceActivationException: The service '/WcfService1/Service1.svc' cannot be activated due to an exception during compilation.  The exception message is: The service cannot be activated because it does not support ASP.NET compatibility. ASP.NET compatibility is enabled for this application. Turn off ASP.NET compatibility mode in the web.config or add the AspNetCompatibilityRequirements attribute to the service type with RequirementsMode setting as 'Allowed' or 'Required'..]
   System.Runtime.AsyncResult.End(IAsyncResult result) +889824
   System.ServiceModel.Activation.HostedHttpRequestAsyncResult.End(IAsyncResult result) +179150
   System.Web.CallHandlerExecutionStep.OnAsyncHandlerCompletion(IAsyncResult ar) +136</pre>
</p>

<hr size="1" width="100%" /><b>Version Information:</b> Microsoft .NET Framework Version:4.0.30128; ASP.NET Version:4.0.30128.
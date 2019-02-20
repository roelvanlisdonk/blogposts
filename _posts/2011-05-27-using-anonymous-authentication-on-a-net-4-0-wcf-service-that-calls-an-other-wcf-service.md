---
ID: 2074
post_title: >
  Using anonymous authentication on a .NET
  4.0 WCF service that calls another WCF
  service
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/05/27/using-anonymous-authentication-on-a-net-4-0-wcf-service-that-calls-an-other-wcf-service/
published: true
post_date: 2011-05-27 11:15:44
---
<p>Let’s say you created a ASP .NET 4.0 website that uses a WCF service to get data from a Microsoft SQL Server database.</p>  <p>The website uses anonymous authentication and you are asked to show data on the website from another WCF service that use anonymous authentication:</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image22.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image_thumb22.png" width="531" height="639" /></a></p>  <p>&#160;</p>  <p>By default wsHttpBinding uses windows authentication, so if you want to use wsHttpBinding in this scenario, you will have to disable authentication on both the WCF Server [A] binding as the WCF Service [B] binding.</p>  <p>This can be done, by setting the security mode to none on the binding and setting clientCredentialType to None on the transport and message nodes:</p>  <p>&#160;</p>  <p><strong>WCF Service [A] Web.config:</strong></p>  <pre class="code"><span style="color: blue">&lt;</span><span style="color: #a31515">system.serviceModel</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">bindings</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">wsHttpBinding</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">binding </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">WSHttpBinding_IMyServiceB</span>&quot; <span style="color: red">closeTimeout</span><span style="color: blue">=</span>&quot;<span style="color: blue">00:01:00</span>&quot; <span style="color: red">openTimeout</span><span style="color: blue">=</span>&quot;<span style="color: blue">00:01:00</span>&quot; <span style="color: red">receiveTimeout</span><span style="color: blue">=</span>&quot;<span style="color: blue">00:10:00</span>&quot; <span style="color: red">sendTimeout</span><span style="color: blue">=</span>&quot;<span style="color: blue">00:01:00</span>&quot; <span style="color: red">bypassProxyOnLocal</span><span style="color: blue">=</span>&quot;<span style="color: blue">false</span>&quot; <span style="color: red">transactionFlow</span><span style="color: blue">=</span>&quot;<span style="color: blue">false</span>&quot; <span style="color: red">hostNameComparisonMode</span><span style="color: blue">=</span>&quot;<span style="color: blue">StrongWildcard</span>&quot; <span style="color: red">maxBufferPoolSize</span><span style="color: blue">=</span>&quot;<span style="color: blue">524288</span>&quot; <span style="color: red">maxReceivedMessageSize</span><span style="color: blue">=</span>&quot;<span style="color: blue">65536</span>&quot; <span style="color: red">messageEncoding</span><span style="color: blue">=</span>&quot;<span style="color: blue">Text</span>&quot; <span style="color: red">textEncoding</span><span style="color: blue">=</span>&quot;<span style="color: blue">utf-8</span>&quot; <span style="color: red">useDefaultWebProxy</span><span style="color: blue">=</span>&quot;<span style="color: blue">true</span>&quot; <span style="color: red">allowCookies</span><span style="color: blue">=</span>&quot;<span style="color: blue">false</span>&quot;<span style="color: blue">&gt;
          &lt;</span><span style="color: #a31515">readerQuotas </span><span style="color: red">maxDepth</span><span style="color: blue">=</span>&quot;<span style="color: blue">32</span>&quot; <span style="color: red">maxStringContentLength</span><span style="color: blue">=</span>&quot;<span style="color: blue">8192</span>&quot; <span style="color: red">maxArrayLength</span><span style="color: blue">=</span>&quot;<span style="color: blue">16384</span>&quot; <span style="color: red">maxBytesPerRead</span><span style="color: blue">=</span>&quot;<span style="color: blue">4096</span>&quot; <span style="color: red">maxNameTableCharCount</span><span style="color: blue">=</span>&quot;<span style="color: blue">16384</span>&quot; <span style="color: blue">/&gt;
          &lt;</span><span style="color: #a31515">reliableSession </span><span style="color: red">ordered</span><span style="color: blue">=</span>&quot;<span style="color: blue">true</span>&quot; <span style="color: red">inactivityTimeout</span><span style="color: blue">=</span>&quot;<span style="color: blue">00:10:00</span>&quot; <span style="color: red">enabled</span><span style="color: blue">=</span>&quot;<span style="color: blue">false</span>&quot; <span style="color: blue">/&gt;
          &lt;</span><span style="color: #a31515">security </span><span style="color: red">mode</span><span style="color: blue">=</span>&quot;<span style="color: blue">None</span>&quot;<span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">transport </span><span style="color: red">clientCredentialType</span><span style="color: blue">=</span>&quot;<span style="color: blue">None</span>&quot; <span style="color: blue">/&gt;
            &lt;</span><span style="color: #a31515">message </span><span style="color: red">clientCredentialType</span><span style="color: blue">=</span>&quot;<span style="color: blue">None</span>&quot; <span style="color: blue">/&gt;
          &lt;/</span><span style="color: #a31515">security</span><span style="color: blue">&gt;
        &lt;/</span><span style="color: #a31515">binding</span><span style="color: blue">&gt;
      &lt;/</span><span style="color: #a31515">wsHttpBinding</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">bindings</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">client</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">endpoint </span><span style="color: red">address</span><span style="color: blue">=</span>&quot;<span style="color: blue">http://localhost:64043/MyServiceB.svc</span>&quot; <span style="color: red">binding</span><span style="color: blue">=</span>&quot;<span style="color: blue">wsHttpBinding</span>&quot; <span style="color: red">bindingConfiguration</span><span style="color: blue">=</span>&quot;<span style="color: blue">WSHttpBinding_IMyServiceB</span>&quot; <span style="color: red">contract</span><span style="color: blue">=</span>&quot;<span style="color: blue">ADAICT.IMyServiceB</span>&quot; <span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">WSHttpBinding_IMyServiceB</span>&quot; <span style="color: blue">/&gt;
    &lt;/</span><span style="color: #a31515">client</span><span style="color: blue">&gt;
</span></pre>


<p>&#160;</p>

<p><strong>WCF Service [B] Web.config</strong></p>

<pre class="code"><span style="color: blue">&lt;</span><span style="color: #a31515">system.serviceModel</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">serviceHostingEnvironment </span><span style="color: red">multipleSiteBindingsEnabled</span><span style="color: blue">=</span>&quot;<span style="color: blue">true</span>&quot; <span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">bindings</span><span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">wsHttpBinding</span><span style="color: blue">&gt;
</span><span style="color: blue">                &lt;</span><span style="color: #a31515">binding </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">AnonymousBinding</span>&quot;<span style="color: blue">&gt;
                  &lt;</span><span style="color: #a31515">security </span><span style="color: red">mode</span><span style="color: blue">=</span>&quot;<span style="color: blue">None</span>&quot;<span style="color: blue">&gt;
                    &lt;</span><span style="color: #a31515">transport </span><span style="color: red">clientCredentialType</span><span style="color: blue">=</span>&quot;<span style="color: blue">None</span>&quot; <span style="color: blue">/&gt;
                    &lt;</span><span style="color: #a31515">message </span><span style="color: red">clientCredentialType</span><span style="color: blue">=</span>&quot;<span style="color: blue">None</span>&quot; <span style="color: blue">/&gt;
                  &lt;/</span><span style="color: #a31515">security</span><span style="color: blue">&gt;
                &lt;/</span><span style="color: #a31515">binding</span><span style="color: blue">&gt;
            &lt;/</span><span style="color: #a31515">wsHttpBinding</span><span style="color: blue">&gt;
        &lt;/</span><span style="color: #a31515">bindings</span><span style="color: blue">&gt;
</span></pre>

<p>…</p>

<p>…</p>

<pre class="code"> <span style="color: blue">&lt;</span><span style="color: #a31515">service </span><span style="color: red">behaviorConfiguration</span><span style="color: blue">=</span>&quot;<span style="color: blue">WcfServiceBehavior</span>&quot; <span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">MyServiceB</span>&quot;<span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">endpoint </span><span style="color: red">binding</span><span style="color: blue">=</span>&quot;<span style="color: blue">wsHttpBinding</span>&quot; <span style="color: red">bindingConfiguration</span><span style="color: blue">=</span>&quot;<span style="color: blue">AnonymousBinding</span>&quot;
              <span style="color: red">contract</span><span style="color: blue">=</span>&quot;<span style="color: blue">IMyServiceB</span>&quot; <span style="color: blue">/&gt;
            &lt;</span><span style="color: #a31515">endpoint </span><span style="color: red">address</span><span style="color: blue">=</span>&quot;<span style="color: blue">mex</span>&quot; <span style="color: red">binding</span><span style="color: blue">=</span>&quot;<span style="color: blue">mexHttpBinding</span>&quot; <span style="color: red">bindingConfiguration</span><span style="color: blue">=</span>&quot;&quot;
              <span style="color: red">contract</span><span style="color: blue">=</span>&quot;<span style="color: blue">IMetadataExchange</span>&quot; <span style="color: blue">/&gt;
            &lt;</span><span style="color: #a31515">host</span><span style="color: blue">&gt;
              &lt;</span><span style="color: #a31515">timeouts </span><span style="color: red">openTimeout</span><span style="color: blue">=</span>&quot;<span style="color: blue">23:59:59</span>&quot; <span style="color: blue">/&gt;
            &lt;/</span><span style="color: #a31515">host</span><span style="color: blue">&gt;
          &lt;/</span><span style="color: #a31515">service</span><span style="color: blue">&gt;
</span></pre>


<p>This allows the WCF Service [A] to communicate with WCF Service [B] on wsHttpBinding with anonymous access.</p>
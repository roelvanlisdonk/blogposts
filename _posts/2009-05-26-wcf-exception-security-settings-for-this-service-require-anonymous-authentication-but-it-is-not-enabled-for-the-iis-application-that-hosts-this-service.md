---
ID: 507
post_title: 'WCF exception: Security settings for this service require &#039;Anonymous&#039; Authentication but it is not enabled for the IIS application that hosts this service.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/26/wcf-exception-security-settings-for-this-service-require-anonymous-authentication-but-it-is-not-enabled-for-the-iis-application-that-hosts-this-service/
published: true
post_date: 2009-05-26 14:38:14
---
<p>Security settings for this service require 'Anonymous' Authentication but it is not enabled for the IIS application that hosts this service.    <br />    <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/05/image13.png"><img style="border-right-width: 0px; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/05/image-thumb13.png" width="244" height="188" /></a>     <br />    <br />    <br />This error occurred, because I had an endpoint configured in mine wcf service web.config with a identity tag, as shown below:</p>  <pre class="code"><span style="color: blue">&lt;</span><span style="color: #a31515">endpoint </span><span style="color: red">address</span><span style="color: blue">=</span>&quot;&quot; <span style="color: red">binding</span><span style="color: blue">=</span>&quot;<span style="color: blue">wsHttpBinding</span>&quot; <span style="color: red">contract</span><span style="color: blue">=</span>&quot;<span style="color: blue">Tpp.Pegaso.MaintenanceService.IMaintenanceService</span>&quot;<span style="color: blue">&gt;
</span><span style="color: blue">    &lt;</span><span style="color: #a31515">identity</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">dns </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">localhost</span>&quot;<span style="color: blue">/&gt;
    &lt;/</span><span style="color: #a31515">identity</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">endpoint</span><span style="color: blue">&gt;</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>This identity element should be removed or replaced to reflect the identity under which the deployed service runs. If removed, WCF will infer an appropriate identity automatically.
  <br />

  <br />To avoid disclosing metadata information, I set the serviceMetadata httpGetEnabled to false:

  <br /><span style="color: blue">&lt;</span><span style="color: #a31515">serviceMetadata </span><span style="color: red">httpGetEnabled</span><span style="color: blue">=</span>&quot;<span style="color: blue">true</span>&quot;<span style="color: blue">/&gt;</span>

  <br />

  <br />and removed the mex endpoint:

  <br /><span style="color: blue">&lt;</span><span style="color: #a31515">endpoint</span><span style="color: red">address</span><span style="color: blue">=</span>&quot;<span style="color: blue">mex</span>&quot; <span style="color: red">binding</span><span style="color: blue">=</span>&quot;<span style="color: blue">mexHttpBinding</span>&quot; <span style="color: red">contract</span><span style="color: blue">=</span>&quot;<span style="color: blue">IMetadataExchange</span>&quot;<span style="color: blue">/&gt;</span></p>
<a href="http://11011.net/software/vspaste"></a><a href="http://11011.net/software/vspaste"></a>
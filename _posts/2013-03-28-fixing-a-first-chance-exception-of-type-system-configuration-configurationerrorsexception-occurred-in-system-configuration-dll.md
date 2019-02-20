---
ID: 3179
post_title: 'Fixing &#8211; A first chance exception of type &#8216;System.Configuration.ConfigurationErrorsException&#8217; occurred in System.Configuration.dll'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/03/28/fixing-a-first-chance-exception-of-type-system-configuration-configurationerrorsexception-occurred-in-system-configuration-dll/
published: true
post_date: 2013-03-28 14:17:00
---
<p>After some NuGet package update, my Web.config file was altered and contained two entries in [connectionStrings] with the same name:</p>  <pre class="code"><p><span style="background: white; color: blue">&lt;</span><span style="background: white; color: #a31515">connectionStrings</span><span style="background: white; color: blue">&gt;
    &lt;</span><span style="background: white; color: #a31515">add </span><span style="background: white; color: red">name</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">DefaultConnection</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">providerName</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">System.Data.SqlClient</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: red">connectionString</span><span style="background: white; color: blue">=</span><span style="background: white; color: black">&quot;</span><span style="background: white; color: blue">data source=s02.dev.nl\v2012;initial catalog=Test;Integrated Security=SSPI;Pooling=False;</span><span style="background: white; color: black">&quot; </span><span style="background: white; color: blue">/&gt;
    &lt;add name=&quot;DefaultConnection&quot; providerName=&quot;System.Data.SqlClient&quot; connectionString=&quot;Data Source=.\SQLEXPRESS;Initial Catalog=aspnet-Test.UI-20130328110613;Integrated Security=SSPI&quot; /&gt;</span></p><p><span style="background: white; color: blue"></span><span style="background: white; color: blue">&lt;/</span><span style="background: white; color: #a31515">connectionStrings</span><span style="background: white; color: blue">&gt;</span></p></pre>


<p>After removing one of the entries, the error was resolved.</p>
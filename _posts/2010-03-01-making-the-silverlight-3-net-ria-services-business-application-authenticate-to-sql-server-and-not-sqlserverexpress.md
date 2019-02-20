---
ID: 1046
post_title: >
  Making the Silverlight 3 .NET RIA
  Services Business Application,
  authenticate to SQL Server and not
  SQLServerExpress
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/01/making-the-silverlight-3-net-ria-services-business-application-authenticate-to-sql-server-and-not-sqlserverexpress/
published: true
post_date: 2010-03-01 21:30:42
---
If you’re are using SQL Server Developer edition to develop a Silverlight 3 .NET RIA Services Business Application you might encounter an exception during login:

Load operation failed for query ‘Login’.

at System.Web.DomainServices.ReflectionDomainServiceDescriptionProvider.ReflectionDomainOperationEntry.Invoke(DomainService domainService, Object[] parameters)
   at System.Web.DomainServices.DomainOperationEntry.Invoke(DomainService domainService, Object[] parameters, Int32&amp; totalCount)
   at System.Web.DomainServices.DomainService.Query(QueryDescription queryDescription, IEnumerable`1&amp; validationErrors, Int32&amp; totalCount)
   at System.Web.Ria.Services.QueryOperationBehavior`1.QueryOperationInvoker.InvokeCore(Object instance, Object[] inputs, Object[]&amp; outputs)

This is because the providers make use of the connectionstring with the name [LocalSqlServer] from you’re machine.config by default this contains the .\SQLServerExpress instead of MSQLServer, you can change this by editing the web.config:
<pre class="code"><span style="color: blue;">&lt;</span><span style="color: #a31515;">connectionStrings</span><span style="color: blue;">&gt;
        &lt;</span><span style="color: #a31515;">remove </span><span style="color: red;">name</span><span style="color: blue;">=</span>"<span style="color: blue;">LocalSqlServer</span>"<span style="color: blue;">/&gt;
        &lt;</span><span style="color: #a31515;">add </span><span style="color: red;">name</span><span style="color: blue;">=</span>"<span style="color: blue;">LocalSqlServer</span>"  <span style="color: red;">connectionString</span><span style="color: blue;">=</span>"<span style="color: blue;">Data Source=.;Initial Catalog=YoureTestDb;Integrated Security=True</span>"    <span style="color: red;">providerName</span><span style="color: blue;">=</span>"<span style="color: blue;">System.Data.SqlClient</span>"<span style="color: blue;">/&gt;
</span><span style="color: blue;">&lt;/</span><span style="color: #a31515;">connectionStrings</span><span style="color: blue;">&gt;</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<strong>Note:</strong>

Make sure the “YoureTestDb” contain the “aspnet_…” authentication tables, by using: C:\Windows\Microsoft.NET\Framework\v2.0.50727&gt;Aspnet_regsql.exe

To install all functionality on a specific database use:
"C:\Windows\Microsoft.NET\Framework\v2.0.50727\Aspnet_regsql.exe" -S MyServer -E -d MyDatabase -A all

If you only want to add membership and roles use:

"C:\Windows\Microsoft.NET\Framework\v2.0.50727\Aspnet_regsql.exe" -S MyServer -E -d MyDatabase -A mr

Don't forget to do an <strong>iisreset</strong>

see: <a href="http://msdn.microsoft.com/en-us/library/x28wfk74.aspx">http://msdn.microsoft.com/en-us/library/x28wfk74.aspx</a>
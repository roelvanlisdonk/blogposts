---
ID: 852
post_title: >
  Exception on Microsoft SQL Server
  Reporting Services PrepareQuery
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/12/15/exception-on-microsoft-sql-server-reporting-services-preparequery/
published: true
post_date: 2009-12-15 11:56:45
---
<p>If you get the exception:   <br />    <br />{&quot;System.Web.Services.Protocols.SoapException: Cannot create a connection to data source ''. ---&gt; Microsoft.ReportingServices.Diagnostics.Utilities.DataSourceOpenException: Cannot create a connection to data source ''. ---&gt; Microsoft.ReportingServices.DataExtensions.ReportServerDataProvider.RSDPException: You have specified integrated security or credentials in the connection string for the data source, but the data source is configured to use a different credential type. To use the values in the connection string, you must configure the unattended report processing account for the report server.\n&#160;&#160; at Microsoft.ReportingServices.WebServer.ReportingService2005Impl.PrepareQuery(DataSource DataSource, DataSetDefinition DataSet, DataSetDefinition&amp; DataSettings, Boolean&amp; Changed, String[]&amp; ParameterNames)\n&#160;&#160; at Microsoft.ReportingServices.WebServer.ReportingService2005.PrepareQuery(DataSource DataSource, DataSetDefinition DataSet, DataSetDefinition&amp; DataSettings, Boolean&amp; Changed, String[]&amp; ParameterNames)&quot;}    <br />    <br />Removing : integrated security=true from mine connection string solved this exception, but then an other exception occurred:    <br />    <br />{&quot;System.Web.Services.Protocols.SoapException: Cannot create a connection to data source ''. ---&gt; Microsoft.ReportingServices.Diagnostics.Utilities.DataSourceOpenException: Cannot create a connection to data source ''. ---&gt; System.Data.SqlClient.SqlException: Login failed for user 'TTUser'.\n&#160;&#160; at Microsoft.ReportingServices.WebServer.ReportingService2005Impl.PrepareQuery(DataSource DataSource, DataSetDefinition DataSet, DataSetDefinition&amp; DataSettings, Boolean&amp; Changed, String[]&amp; ParameterNames)\n&#160;&#160; at Microsoft.ReportingServices.WebServer.ReportingService2005.PrepareQuery(DataSource DataSource, DataSetDefinition DataSet, DataSetDefinition&amp; DataSettings, Boolean&amp; Changed, String[]&amp; ParameterNames)&quot;}    <br />    <br />This can be caused by getting a datasourcedefinition instead of creating a datasourcedefinition. <strong><font color="#ff0000">When getting a datasourcedefinition the Password will be reset to NULL</font></strong>, resetting the password solves this exception:    <br /></p>  <pre class="code"><span style="color: green">// Get the shared datasource.
</span><span style="color: #2b91af">DataSourceDefinition </span>dataSourceDefinition = rs.GetDataSourceContents(“TestSharedDataSource”);

<span style="color: green">// Reset password
</span>dataSourceDefinition.Password = “mypassword”;</pre>
<a href="http://11011.net/software/vspaste"></a>
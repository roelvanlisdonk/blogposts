---
ID: 5223
post_title: 'Fix: Visual Studio Test project &#8211; The Entity Framework provider type &#8216;System.Data.Entity.SqlServer.SqlProviderServices, EntityFramework.SqlServer&#8217; registered in the application config'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2018/07/04/fix-visual-studio-test-project-the-entity-framework-provider-type-system-data-entity-sqlserver-sqlproviderservices-entityframework-sqlserver-registered-in-the-application-config/
published: true
post_date: 2018-07-04 15:37:39
---
<p>
 </p><p>After installing the NugetPackage EntityFramework in a .NET 4.5.2 Visual Studio Test project, using an EntityFramework DbContext would throw an exception during test run: 
</p><p>
 </p><p><span style="color:red">The Entity Framework provider type 'System.Data.Entity.SqlServer.SqlProviderServices, EntityFramework.SqlServer' registered in the application config file for the ADO.NET provider with invariant name 'System.Data.SqlClient' could not be loaded. Make sure that the assembly-qualified name is used and that the assembly is available to the running application. See http://go.microsoft.com/fwlink/?LinkId=260882 for more information.
</span></p><p>
 </p><p>This can be fixed, by touching the System.Data.Entity.SqlServer.SqlProviderServices.Instance in your test project, e.g. by adding a property that returns the System.Data.Entity.SqlServer.SqlProviderServices.Instance to the Test class.
</p><p>
 </p><p>[TestClass]
</p><p>public class MyTest
</p><p>{
</p><p>
 </p><p>        public System.Data.Entity.SqlServer.SqlProviderServices SqlServerInstance { get { return <span style="color:red">System.Data.Entity.SqlServer.SqlProviderServices.Instance</span>; } }
</p><p>}
</p><p>
 </p><p>
 </p><p>More information can be found at:
</p><p>http://robsneuron.blogspot.com/2013/11/entity-framework-upgrade-to-6.html
</p><p> 
 </p><p>
 </p>
---
ID: 2607
post_title: >
  Using SQL Server 2012 LocalDb in VS11
  and VS2010 for testing.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/03/19/using-sql-server-2012-localdb-in-vs11-for-testing/
published: true
post_date: 2012-03-19 21:57:18
---
<p>To create high quality LOB applications unit tests and integration tests are mandatory. You want to run these integration tests and unit tests on your continuous integration server. The problem with integration tests or testing things like stored procedures you want your database filled with consistent test data and you don’t want multiple tests ore multiple builds have impact on each other. To prevent this, you can run a SQL script that deploys a new database for each test, creating a unique database with test data and after running the tests delete this database. This is a whole lot of work and it can be simplified and improving performance by using a LocalDb file, instead of a SQL Server test instance.</p>  <p>&#160;</p>  <h3><font style="font-weight: bold">LocalDb benefits</font></h3>  <p>- No SQL Server installation for running integration tests or testing stored procedures, on your local dev machine or on the continuous build server.</p>  <p>- Improved performance for tests (uses share memory, instead of TCP / IP to connect to database).</p>  <p>- Increase in speed of development.</p>  <p>- No code (T-SQL, EF etc.) changes, because LocalDb contains the same functionality as the full blown SQL Server (same code base).</p>  <p>- No configuration</p>  <p>- Supports AttachDBFileName, this means you can automatically copy the LocalDb (containing you test data) to your test output folder, by using the standard [DeploymentItems] and then let the integration tests use this file to connect to.</p>  <p>- It’s FREE</p>  <p>- Works on &gt;= Visual Studio 2010</p>  <p>&#160;</p>  <h3><font style="font-weight: bold">LocalDb disadvantages</font></h3>  <p>- Requires .NET 4.0.2</p>  <p>&#160;</p>  <h2>Instructions for VS11</h2>  <p>To show the usage of the Microsoft SQL Server 2012 LocalDb file in a Microsoft Visual Studio test project, you can use the following instructions:</p>  <p>&#160;</p>  <p><strong>Create a Microsoft Visual Studio Solution</strong></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image16.png" rel="lightbox"><img style="background-image: none; border-right-width: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image_thumb16.png" width="580" height="518" /></a></p>  <p>&#160;</p>  <p><strong>Create a resources project, containing the LocalDb file</strong></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image17.png" rel="lightbox"><img style="background-image: none; border-right-width: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image_thumb17.png" width="580" height="405" /></a></p>  <p><strong></strong></p>  <p><strong>Add a Microsoft SQL Server 2012 LocalDb file</strong></p>  <p>Add &gt; New Item… &gt; Visual C# Items &gt; Data &gt; Service-based Database:</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image18.png" rel="lightbox"><img style="background-image: none; border-right-width: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image_thumb18.png" width="580" height="405" /></a></p>  <p>Just click Next &gt; Next &gt; Finish:</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image19.png" rel="lightbox"><img style="background-image: none; border-right-width: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image_thumb19.png" width="453" height="352" /></a></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image20.png" rel="lightbox"><img style="background-image: none; border-right-width: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image_thumb20.png" width="456" height="354" /></a></p>  <p>Remove the dataset: LocalDbDemoDataSet.xsd</p>  <p>&#160;</p>  <p><strong>Add a Unit test project, containing tests, that connect to the LocalDb file</strong></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image21.png" rel="lightbox"><img style="background-image: none; border-right-width: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image_thumb21.png" width="580" height="407" /></a></p>  <p>&#160;</p>  <p><strong>Add a *.testsetting file to you solution</strong></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image22.png" rel="lightbox"><img style="background-image: none; border-right-width: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image_thumb22.png" width="580" height="326" /></a></p>  <p>&#160;</p>  <p><strong>Enable DeploymentItems and add LocalDb to deployment items</strong></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image23.png" rel="lightbox"><img style="background-image: none; border-right-width: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image_thumb23.png" width="580" height="429" /></a></p>  <p>This will copy the LocalDbDemo.mdf and ldf file to the Microsoft Visual Studio output folder. So the only code that can interfere with your test data and test database, are your own tests. If you want a clean database not for each test run, but foreach test, then you can use the DeploymentItem attribute on your test or test class.&#160; </p>  <p>&#160;</p>  <p><strong>Add a unit test class [LocalDbTester] to the test project</strong></p>  <p>By using the [AttachDbFilename] property in your connection string, the test will automatically attach the *.mdf and *.ldf file to the LocalDb engine. Note: without specifying the Initial Catalog or Database property, the name of the database will include the full path to the *.mdf file, in most cases this is not what you want.</p>  <p>&#160;</p>  <p><strong>Final solution setup, should look like:</strong></p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image24.png" rel="lightbox"><img style="background-image: none; border-right-width: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image_thumb24.png" width="398" height="510" /></a></p>  <p><strong></strong></p>  <p><strong>Run the test</strong></p>  <p>The output is a succeeded test, demonstrating connecting to the LocalDb *.mdf file, within a Microsoft Visual Studio 11 test project.</p>  <pre class="code"><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Data;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Data.SqlClient;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.IO;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Reflection;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Microsoft.VisualStudio.TestTools.UnitTesting;

</span><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">LocalDbDemo.Test
{
    [</span><span style="background: white; color: #2b91af">TestClass</span><span style="background: white; color: black">]
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">LocalDbTester
    </span><span style="background: white; color: black">{
        [</span><span style="background: white; color: #2b91af">TestMethod</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">ShowLocalDbData()
        {
            </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">mdfFilename = </span><span style="background: white; color: maroon">&quot;LocalDbDemo.mdf&quot;</span><span style="background: white; color: black">;
            </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">outputFolder = </span><span style="background: white; color: #2b91af">Path</span><span style="background: white; color: black">.GetDirectoryName(</span><span style="background: white; color: #2b91af">Assembly</span><span style="background: white; color: black">.GetExecutingAssembly().Location);
            </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">attachDbFilename = </span><span style="background: white; color: #2b91af">Path</span><span style="background: white; color: black">.Combine(outputFolder, mdfFilename);
            </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">connectionString = </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">@&quot;Data Source=(LocalDB)\v11.0;Initial Catalog=LocalDbDemo;AttachDbFilename=&quot;&quot;{0}&quot;&quot;;Integrated Security=True&quot;</span><span style="background: white; color: black">, attachDbFilename);
            </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">connection = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">SqlConnection</span><span style="background: white; color: black">(connectionString))
            </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">command = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">SqlCommand</span><span style="background: white; color: black">(</span><span style="background: white; color: maroon">&quot;select * from Person&quot;</span><span style="background: white; color: black">, connection))
            </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">adapter = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">SqlDataAdapter</span><span style="background: white; color: black">(command))
            {
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">table = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">DataTable</span><span style="background: white; color: black">();
                </span><span style="background: white; color: blue">int </span><span style="background: white; color: black">count = adapter.Fill(table);
                </span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">.IsTrue(count &gt; 0);
            }
        }
    }
}</span></pre>

<h2>Instructions for VS2010</h2>

<p align="left">The instructions for VS11, also apply for Microsoft Visual Studio 2010, but there are some prerequisites:</p>

<p align="left">- Microsoft Visual Studio 2010 SP1, should be installed (<a href="http://www.microsoft.com/download/en/details.aspx?id=23691">http://www.microsoft.com/download/en/details.aspx?id=23691</a>).</p>

<p align="left">- Microsoft .NET 4.0.2 design-time update (for developer machine <a href="http://www.microsoft.com/download/en/details.aspx?id=27759">http://www.microsoft.com/download/en/details.aspx?id=27759</a>). </p>

<p align="left">- Microsoft .NET 4.0.2 run-time update (for machines that do not contain Microsoft Visual Studio 2010 <a href="http://www.microsoft.com/download/en/details.aspx?displaylang=en&amp;id=27756">http://www.microsoft.com/download/en/details.aspx?displaylang=en&amp;id=27756</a>).</p>

<p align="left">- SqlLocalDb.msi (<a href="http://msdn.microsoft.com/en-us/evalcenter/hh230763">http://msdn.microsoft.com/en-us/evalcenter/hh230763</a>):</p>

<p align="left">&#160;</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image25.png" rel="lightbox"><img style="background-image: none; border-right-width: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image_thumb25.png" width="568" height="436" /></a></p>

<p>&#160;</p>

<p>&#160;</p>

<p><strong>Some extra instructions for Visual Studio 2010</strong></p>

<p>Creating a LocalDb file in C:\Users\&lt;UserAccountName&gt;…, use the Server Explorer:</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image27.png" rel="lightbox"><img style="background-image: none; border-right-width: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image_thumb27.png" width="312" height="466" /></a></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image28.png" rel="lightbox"><img style="background-image: none; border-right-width: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image_thumb28.png" width="372" height="162" /></a></p>

<p>A LocalDbDemo.mdf and LocalDbDemo.ldf file will be created in the folder C:\Users\&lt;UserAccountName&gt;…</p>

<p>These files can now be copied and included in the LocalDbDemo.Resource project.</p>

<p>Adding a new LocalDb file by using the Add New Item &gt; Data &gt; Service-based Database, will not work in VS2010:</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image26.png" rel="lightbox"><img style="background-image: none; border-right-width: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image_thumb26.png" width="580" height="400" /></a></p>

<p>&#160;</p>

<p>Managing the localdb (creating tables, stored procedures etc.), should be done by using Microsoft SQL Server 2012 Management studio. Just connect to (localdb\V11.0) and then attach the created localdb file.</p>

<p>&#160;</p>

<p><strong>End results in Microsoft Visual 2010</strong></p>

<p>This screen dump shows the use of a LocalDb.mdf file in a Microsoft Visual Studio 2010 unit test.</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image29.png" rel="lightbox"><img style="background-image: none; border-right-width: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image_thumb29.png" width="580" height="326" /></a></p>

<p>So using Microsoft SQL Server 2012 LocalDb in a Microsoft Visual Studio 2010 unit test works.</p>

<p>&#160;</p>

<p><strong>Notes</strong></p>

<p>One of the big disadvantages of using Microsoft Visual Studio 2010 instead of Microsoft Visual Studio 11, is that the LocalDb.mdf file can’t be edited / designed by using Microsoft Visual Studio 2010 directly, you must use Microsoft SQL Server 2012 Management Studio to edit / design the database.</p>

<p>If you encounter attach error, because the localdb is already attached, read my other post on changing the database file paths of an online localdb databaes (<a href="http://www.roelvanlisdonk.nl/?p=2636">http://www.roelvanlisdonk.nl/?p=2636</a>).</p>

<p>&#160;</p>

<p><strong>More information on LocalDb:</strong></p>

<p><a href="http://channel9.msdn.com/posts/SQL11UPD03-REC-07">http://channel9.msdn.com/posts/SQL11UPD03-REC-07</a></p>

<p><a href="http://channel9.msdn.com/posts/SQL11UPD04-REC-02">http://channel9.msdn.com/posts/SQL11UPD04-REC-02</a></p>
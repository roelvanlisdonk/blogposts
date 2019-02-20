---
ID: 2636
post_title: 'How to change the *.mdf and *.ldf location of an online Microsoft SQL Server LocalDb database in a Microsoft Visual Studio 2010 test.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/03/23/how-to-change-the-mdf-and-ldf-location-of-an-online-microsoft-sql-server-localdb-database-in-a-microsoft-visual-studio-2010-test/
published: true
post_date: 2012-03-23 12:32:41
---
<p>For testing purposes it is possible to copy a new localdb database to your output directory and start using this localdb database. For more information see my previous post: <a href="http://www.roelvanlisdonk.nl/?p=2607">http://www.roelvanlisdonk.nl/?p=2607</a></p>  <p>It is possible that a previous tests run did not cleanup it’s copy of the localdb database. Now if you want to attach an new localdb database with the same name, the attach will fail. There are several options you have to fix this error. I decided to just &quot;re-use&quot; the existing database, just changing the *.mdf and *.ldf file location.</p>  <p>&#160;</p>  <p>The following code can help you do just that:</p>  <pre class="code"><span style="color: blue">using </span>System.Data.SqlClient;
<span style="color: blue">using </span>System.IO;
<span style="color: blue">using </span>System.Reflection;
<span style="color: blue">using </span>Microsoft.VisualStudio.TestTools.UnitTesting;
<span style="color: blue">using </span>System;

<span style="color: blue">namespace </span>Test.Research
{
    <span style="color: gray">/// &lt;summary&gt;
    /// </span><span style="color: green">Tests in this class are only used to analyse and research code.
    </span><span style="color: gray">/// </span><span style="color: green">It is not intended to contain real integration tests.
    </span><span style="color: gray">/// &lt;/summary&gt;
    </span>[<span style="color: #2b91af">TestClass</span>]
    <span style="color: blue">public class </span><span style="color: #2b91af">RliResearchTester</span><span style="color: #2b91af">
    </span>{
        
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Changes the *.mdf and *.ldf file location for the given LocalDb database, when it exists.
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;remarks&gt;
        /// </span><span style="color: green">It expects the mdf file name to be in the format [DatabaseName.mdf].
        </span><span style="color: gray">/// </span><span style="color: green">It expects the ldf file name to be in the format [Databasename_log.ldf].
        </span><span style="color: gray">/// </span><span style="color: green">It expects the old mdf file name to be equal to the new mdf file name (only the file location will change).
        </span><span style="color: gray">/// </span><span style="color: green">It expects the old ldf file name to be equal to the new ldf file name (only the file location will change).
        </span><span style="color: gray">/// &lt;/remarks&gt;
        </span>[<span style="color: #2b91af">TestMethod</span>]
        <span style="color: blue">public void </span>ChangeMdfAndLdfLocationForExistingLocalDb()
        {
            <span style="color: blue">string </span>dataSource = <span style="color: #a31515">@&quot;(localdb)\V11.0&quot;</span>;
            <span style="color: blue">string </span>databaseName = <span style="color: #a31515">&quot;MyReserachDb&quot;</span>;
            <span style="color: blue">string </span>folderContainingNewDatabaseFiles = <span style="color: #2b91af">Path</span>.GetDirectoryName(<span style="color: #2b91af">Assembly</span>.GetExecutingAssembly().Location);
            <span style="color: blue">string </span>oldMdfFilePath = GetMdfFilePath(dataSource, databaseName);
            <span style="color: blue">if </span>(!<span style="color: blue">string</span>.IsNullOrWhiteSpace(oldMdfFilePath))
            {
                ModifyDatabaseFilePaths(dataSource, databaseName, folderContainingNewDatabaseFiles);
            }
        }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Gets the full physical mdf filepath, based on the supplied data soruce (Servername\Instancename) and database name.
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;dataSource&quot;&gt;</span><span style="color: green">SQL Server instance in the format (ServerName\InstanceName)</span><span style="color: gray">&lt;/param&gt;
        /// &lt;param name=&quot;databaseName&quot;&gt;</span><span style="color: green">Name of the database.</span><span style="color: gray">&lt;/param&gt;
        /// &lt;returns&gt;
        /// </span><span style="color: green">Databse found:     Returns the full physical mdf filepath.
        </span><span style="color: gray">/// </span><span style="color: green">Databse not found: Returns null.
        </span><span style="color: gray">/// &lt;/returns&gt;
        /// &lt;remarks&gt;
        /// </span><span style="color: green">Uses windows authentication to connect.
        </span><span style="color: gray">/// </span><span style="color: green">This function does not take into account, the fact that a mdf file name can be different, then the [DatabaseName.mdf].
        </span><span style="color: gray">/// &lt;/remarks&gt;
        </span><span style="color: blue">public string </span>GetMdfFilePath(<span style="color: blue">string </span>dataSource, <span style="color: blue">string </span>databaseName)
        {
            <span style="color: blue">string </span>result = <span style="color: blue">null</span>;
            <span style="color: blue">string </span>mdfName = databaseName;
            <span style="color: blue">using </span>(<span style="color: blue">var </span>connection = <span style="color: blue">new </span><span style="color: #2b91af">SqlConnection</span>(<span style="color: blue">string</span>.Format(<span style="color: #a31515">@&quot;Data Source=&quot;&quot;{0}&quot;&quot;;Initial Catalog=master;Integrated Security=True;&quot;</span>, dataSource)))
            <span style="color: blue">using </span>(<span style="color: blue">var </span>command = <span style="color: blue">new </span><span style="color: #2b91af">SqlCommand</span>(<span style="color: #a31515">&quot;select top 1 physical_name from sys.master_files where name = @MdfName&quot;</span>, connection))
            {
                command.Parameters.Add(<span style="color: blue">new </span><span style="color: #2b91af">SqlParameter</span>(<span style="color: #a31515">&quot;MdfName&quot;</span>, mdfName));

                connection.Open();
                result = command.ExecuteScalar() <span style="color: blue">as string</span>;
            }
            <span style="color: blue">return </span>result;
        }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Modifies the *.mdf and *.ldf database file locations of an existing online database.
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;dataSource&quot;&gt;</span><span style="color: green">SQL Server instance in the format (ServerName\InstanceName)</span><span style="color: gray">&lt;/param&gt;
        /// &lt;param name=&quot;databaseName&quot;&gt;</span><span style="color: green">Name of the database.</span><span style="color: gray">&lt;/param&gt;
        /// &lt;param name=&quot;folderContainingNewDatabaseFiles&quot;&gt;</span><span style="color: green">The folder containing new database files.</span><span style="color: gray">&lt;/param&gt;
        /// &lt;remarks&gt;
        /// </span><span style="color: green">- Uses windows authentication to connect.
        </span><span style="color: gray">/// </span><span style="color: green">- Drops all existing database connections, by using [with rollback immediate] on the [set offline].
        </span><span style="color: gray">/// </span><span style="color: green">- Forces the database to use the new files, by using [set offline] and [set online].
        </span><span style="color: gray">/// </span><span style="color: green">- It expects the mdf file name to be in the format [DatabaseName.mdf].
        </span><span style="color: gray">/// </span><span style="color: green">- It expects the ldf file name to be in the format [Databasename_log.ldf].
        </span><span style="color: gray">/// </span><span style="color: green">- It expects the old mdf file name to be equal to the new mdf file name (only the file location will change).
        </span><span style="color: gray">/// </span><span style="color: green">- It expects the old ldf file name to be equal to the new ldf file name (only the file location will change).
        </span><span style="color: gray">/// &lt;/remarks&gt;
        </span><span style="color: blue">public void </span>ModifyDatabaseFilePaths(<span style="color: blue">string </span>dataSource, <span style="color: blue">string </span>databaseName, <span style="color: blue">string </span>folderContainingNewDatabaseFiles)
        {
            <span style="color: blue">string </span>mdfName = databaseName;
            <span style="color: blue">string </span>ldfName = <span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;{0}_log&quot;</span>, databaseName);
            <span style="color: blue">string </span>newMdfFileLocation = <span style="color: #2b91af">Path</span>.Combine(folderContainingNewDatabaseFiles, <span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;{0}.mdf&quot;</span>, mdfName));
            <span style="color: blue">string </span>newLdfFileLocation = <span style="color: #2b91af">Path</span>.Combine(folderContainingNewDatabaseFiles, <span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;{0}.ldf&quot;</span>, ldfName));
            <span style="color: blue">string </span>query = <span style="color: blue">string</span>.Format(<span style="color: #a31515">@&quot;
                alter database {0} modify file (name = {1}, filename = '{3}');
                alter database {0} modify file (name = {2}, filename = '{4}');
                alter database {0} set offline with rollback immediate;
                alter database {0} set online;&quot;</span>, 
                <span style="color: blue">new string</span>[] { databaseName, mdfName, ldfName, newMdfFileLocation, newLdfFileLocation });
            <span style="color: blue">using </span>(<span style="color: blue">var </span>connection = <span style="color: blue">new </span><span style="color: #2b91af">SqlConnection</span>(<span style="color: blue">string</span>.Format(<span style="color: #a31515">@&quot;Data Source=&quot;&quot;{0}&quot;&quot;;Initial Catalog=master;Integrated Security=True;&quot;</span>, dataSource)))
            <span style="color: blue">using </span>(<span style="color: blue">var </span>command = <span style="color: blue">new </span><span style="color: #2b91af">SqlCommand</span>(query, connection))
            {
                connection.Open();
                command.ExecuteNonQuery();
            }
        }
    }
}</pre>
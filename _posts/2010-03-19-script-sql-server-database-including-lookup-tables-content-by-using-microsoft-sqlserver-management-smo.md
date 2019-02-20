---
ID: 1141
post_title: >
  Script SQL Server database, including
  lookup tables content, by using
  Microsoft.SqlServer.Management.Smo
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/19/script-sql-server-database-including-lookup-tables-content-by-using-microsoft-sqlserver-management-smo/
published: true
post_date: 2010-03-19 09:57:14
---
<p>If you want to script a SQL Server database and want to include content for the lookup tables, you can use Microsoft.SqlServer.Management.Smo in C#:</p> <ul> <li>Add reference to Microsoft.SqlServer.Smo  <li>Add reference to Microsoft.SqlServer.ConnectionInfo  <li>Add reference to Microsoft.SqlServer.Management.Sdk.Sfc </li></ul> <p>&nbsp;</p> <p>Use the following code to scripts Tables, Content, Store Procedures and Functions</p><pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Specialized;
<span style="color: blue">using </span>System.Data.SqlClient;
<span style="color: blue">using </span>System.IO;
<span style="color: blue">using </span>System.Text;
<span style="color: blue">using </span>Microsoft.SqlServer.Management.Common;
<span style="color: blue">using </span>Microsoft.SqlServer.Management.Sdk.Sfc;
<span style="color: blue">using </span>Microsoft.SqlServer.Management.Smo;
<span style="color: blue">using </span>NUnit.Framework;

<span style="color: blue">namespace </span>Sales.Test.Database
{
    [<span style="color: #2b91af">TestFixture</span>]
    <span style="color: blue">public class </span><span style="color: #2b91af">ScriptObjects
    </span>{
        [<span style="color: #2b91af">Test</span>]
        <span style="color: blue">public void </span>ScriptDatabaseTest()
        {             
            <span style="color: green">// Reference the SQL Server instance
            </span><span style="color: #2b91af">SqlConnection </span>sqlConnection = <span style="color: blue">new </span><span style="color: #2b91af">SqlConnection</span>(<span style="color: #a31515">"Data Source=.;Initial Catalog=AdaSales;Integrated Security=SSPI;"</span>);
            <span style="color: #2b91af">ServerConnection </span>serverConnection = <span style="color: blue">new </span><span style="color: #2b91af">ServerConnection</span>(sqlConnection);
            <span style="color: #2b91af">Server </span>server = <span style="color: blue">new </span><span style="color: #2b91af">Server</span>(serverConnection);
            
            <span style="color: green">// Reference the database
            </span>Microsoft.SqlServer.Management.Smo.<span style="color: #2b91af">Database </span>database = server.Databases[<span style="color: #a31515">"AdaSales"</span>];
            
            <span style="color: green">// Delete output folder if it exist
            </span><span style="color: #2b91af">DirectoryInfo </span>outputFolder = <span style="color: blue">new </span><span style="color: #2b91af">DirectoryInfo</span>(<span style="color: #a31515">@"C:\Temp"</span>);
            <span style="color: blue">if </span>(outputFolder.Exists) { outputFolder.Delete(<span style="color: blue">true</span>); }

            <span style="color: green">// Create [Output] folder
            </span>outputFolder.Create();

            <span style="color: green">// Create [Tables] output folder
            </span><span style="color: #2b91af">DirectoryInfo </span>tablesOutputFolder = <span style="color: blue">new </span><span style="color: #2b91af">DirectoryInfo</span>(<span style="color: #2b91af">Path</span>.Combine(outputFolder.FullName, <span style="color: #a31515">"Tables"</span>));
            tablesOutputFolder.Create();

            <span style="color: green">// Loop tables
            </span><span style="color: blue">foreach </span>(<span style="color: #2b91af">Table </span>table <span style="color: blue">in </span>database.Tables)
            {
                
                <span style="color: green">// Generate script
                // Include primairykey, foreignkey, constaints, defaults etc.
                // Exclude collation information
                </span><span style="color: #2b91af">StringBuilder </span>resultScript = <span style="color: blue">new </span><span style="color: #2b91af">StringBuilder</span>(<span style="color: blue">string</span>.Empty);

                <span style="color: green">// Only create table when it does not exist
                </span>resultScript.AppendFormat(<span style="color: #a31515">"IF NOT EXISTS (SELECT * FROM sys.objects WHERE object_id = OBJECT_ID(N'[dbo].[{0}]') AND type in (N'U'))"</span>, table.Name).Append(<span style="color: #2b91af">Environment</span>.NewLine);
                resultScript.AppendLine(<span style="color: #a31515">"BEGIN"</span>);

                <span style="color: #2b91af">ScriptingOptions </span>options = <span style="color: blue">new </span><span style="color: #2b91af">ScriptingOptions</span>();
                options.DriAll = <span style="color: blue">true</span>;
                options.NoCollation = <span style="color: blue">true</span>;
                <span style="color: #2b91af">StringCollection </span>scriptLines = table.Script(options);
                
                <span style="color: green">// Add script to file content
                </span><span style="color: blue">foreach </span>(<span style="color: blue">string </span>scriptLine <span style="color: blue">in </span>scriptLines)
                {
                    <span style="color: blue">string </span>line = scriptLine;
                    line = line.Replace(<span style="color: #a31515">"SET ANSI_NULLS ON"</span>, <span style="color: blue">string</span>.Empty);
                    line = line.Replace(<span style="color: #a31515">"SET QUOTED_IDENTIFIER ON"</span>, <span style="color: blue">string</span>.Empty);
                    line = line.Replace(<span style="color: #a31515">"SET ANSI_NULLS OFF"</span>, <span style="color: blue">string</span>.Empty);
                    line = line.Replace(<span style="color: #a31515">"SET QUOTED_IDENTIFIER OFF"</span>, <span style="color: blue">string</span>.Empty);
                    resultScript.AppendLine(line.Trim());
                }

                resultScript.AppendLine(<span style="color: #a31515">"END"</span>);

                <span style="color: green">// Write file content to disk
                </span><span style="color: blue">string </span>fileName = <span style="color: blue">string</span>.Format(<span style="color: #a31515">"{0}.sql"</span>,table.Name);
                <span style="color: #2b91af">File</span>.WriteAllText(<span style="color: #2b91af">Path</span>.Combine(tablesOutputFolder.FullName, fileName), resultScript.ToString());
            }

            <span style="color: green">// Create [Content] output folder
            </span><span style="color: #2b91af">DirectoryInfo </span>contentOutputFolder = <span style="color: blue">new </span><span style="color: #2b91af">DirectoryInfo</span>(<span style="color: #2b91af">Path</span>.Combine(outputFolder.FullName, <span style="color: #a31515">"Content"</span>));
            contentOutputFolder.Create();

            <span style="color: green">// Loop tables for content
            </span><span style="color: blue">foreach </span>(<span style="color: #2b91af">Table </span>table <span style="color: blue">in </span>database.Tables)
            {
                <span style="color: green">// Only include lookup tables
                </span><span style="color: blue">if </span>(table.ForeignKeys.Count == 0)
                {
                    
                    <span style="color: green">// Generate script
                    // Include content in script
                    // Exclude table schema (table creation etc.) and Dri (foreignkeys etc.)
                    </span><span style="color: #2b91af">StringBuilder </span>resultScript = <span style="color: blue">new </span><span style="color: #2b91af">StringBuilder</span>(<span style="color: blue">string</span>.Empty);

                    <span style="color: green">// Only insert data when table is empty
                    </span>resultScript.AppendFormat(<span style="color: #a31515">"IF NOT EXISTS (SELECT 1 FROM [dbo].[{0}])"</span>, table.Name).Append(<span style="color: #2b91af">Environment</span>.NewLine);
                    resultScript.AppendLine(<span style="color: #a31515">"BEGIN"</span>);

                    <span style="color: #2b91af">Scripter </span>scripter = <span style="color: blue">new </span><span style="color: #2b91af">Scripter</span>(server);
                    <span style="color: #2b91af">ScriptingOptions </span>options = <span style="color: blue">new </span><span style="color: #2b91af">ScriptingOptions</span>();
                    options.DriAll = <span style="color: blue">false</span>;
                    options.ScriptSchema = <span style="color: blue">false</span>;
                    options.ScriptData = <span style="color: blue">true</span>;
                    scripter.Options = options;

                    <span style="color: green">// Add script to file content
                    </span><span style="color: blue">foreach </span>(<span style="color: blue">string </span>scriptLine <span style="color: blue">in </span>scripter.EnumScript(<span style="color: blue">new </span><span style="color: #2b91af">Urn</span>[] { table.Urn }))
                    {
                        <span style="color: blue">string </span>line = scriptLine;
                        line = line.Replace(<span style="color: #a31515">"SET ANSI_NULLS ON"</span>, <span style="color: blue">string</span>.Empty);
                        line = line.Replace(<span style="color: #a31515">"SET QUOTED_IDENTIFIER ON"</span>, <span style="color: blue">string</span>.Empty);
                        line = line.Replace(<span style="color: #a31515">"SET ANSI_NULLS OFF"</span>, <span style="color: blue">string</span>.Empty);
                        line = line.Replace(<span style="color: #a31515">"SET QUOTED_IDENTIFIER OFF"</span>, <span style="color: blue">string</span>.Empty);
                        resultScript.AppendLine(line.Trim());
                    }
                    
                    resultScript.AppendLine(<span style="color: #a31515">"END"</span>);

                    <span style="color: green">// Write file content to disk
                    </span><span style="color: blue">string </span>fileName = <span style="color: blue">string</span>.Format(<span style="color: #a31515">"{0}.sql"</span>, table.Name);
                    <span style="color: #2b91af">File</span>.WriteAllText(<span style="color: #2b91af">Path</span>.Combine(contentOutputFolder.FullName, fileName), resultScript.ToString());
                }
            }
            
            <span style="color: green">// Create [Stored Procedures] output folder
            </span><span style="color: #2b91af">DirectoryInfo </span>storedProceduresOutputFolder = <span style="color: blue">new </span><span style="color: #2b91af">DirectoryInfo</span>(<span style="color: #2b91af">Path</span>.Combine(outputFolder.FullName, <span style="color: #a31515">"Stored Procedures"</span>));
            storedProceduresOutputFolder.Create();

            <span style="color: green">// Loop stored procedures
            </span><span style="color: blue">foreach </span>(<span style="color: #2b91af">StoredProcedure </span>storedProcedure <span style="color: blue">in </span>database.StoredProcedures)
            {
                <span style="color: green">// Exclude system stored procedures
                </span><span style="color: blue">if </span>(!storedProcedure.IsSystemObject)
                {
                    <span style="color: green">// Generate script
                    // Include drop statements
                    </span><span style="color: #2b91af">StringBuilder </span>resultScript = <span style="color: blue">new </span><span style="color: #2b91af">StringBuilder</span>(<span style="color: blue">string</span>.Empty);

                    <span style="color: green">// Append drop statement
                    </span>resultScript.AppendFormat(<span style="color: #a31515">"IF EXISTS (SELECT * FROM sys.objects WHERE object_id = OBJECT_ID(N'[dbo].[{0}]') AND type in (N'P', N'PC'))"</span>, storedProcedure.Name).Append(<span style="color: #2b91af">Environment</span>.NewLine);
                    resultScript.AppendLine(<span style="color: #a31515">"BEGIN"</span>);
                    resultScript.AppendFormat(<span style="color: #a31515">"    DROP PROCEDURE [dbo].[{0}]"</span>, storedProcedure.Name).Append(<span style="color: #2b91af">Environment</span>.NewLine);
                    resultScript.AppendLine(<span style="color: #a31515">"END"</span>);
                    resultScript.AppendLine(<span style="color: #a31515">"GO"</span>);

                    <span style="color: green">// Add script to file content
                    </span><span style="color: blue">foreach </span>(<span style="color: blue">string </span>scriptLine <span style="color: blue">in </span>storedProcedure.Script())
                    {
                        <span style="color: blue">string </span>line = scriptLine;
                        line = line.Replace(<span style="color: #a31515">"SET ANSI_NULLS ON"</span>, <span style="color: blue">string</span>.Empty);
                        line = line.Replace(<span style="color: #a31515">"SET QUOTED_IDENTIFIER ON"</span>, <span style="color: blue">string</span>.Empty);
                        line = line.Replace(<span style="color: #a31515">"SET ANSI_NULLS OFF"</span>, <span style="color: blue">string</span>.Empty);
                        line = line.Replace(<span style="color: #a31515">"SET QUOTED_IDENTIFIER OFF"</span>, <span style="color: blue">string</span>.Empty);
                        resultScript.AppendLine(line.Trim());
                    }

                    <span style="color: green">// Write file content to disk
                    </span><span style="color: blue">string </span>fileName = <span style="color: blue">string</span>.Format(<span style="color: #a31515">"{0}.sql"</span>, storedProcedure.Name);
                    <span style="color: #2b91af">File</span>.WriteAllText(<span style="color: #2b91af">Path</span>.Combine(storedProceduresOutputFolder.FullName, fileName), resultScript.ToString());
                }
            }

            <span style="color: green">// Create [Functions] output folder
            </span><span style="color: #2b91af">DirectoryInfo </span>functionsOutputFolder = <span style="color: blue">new </span><span style="color: #2b91af">DirectoryInfo</span>(<span style="color: #2b91af">Path</span>.Combine(outputFolder.FullName, <span style="color: #a31515">"Functions"</span>));
            functionsOutputFolder.Create();

            <span style="color: green">// Loop stored procedures
            </span><span style="color: blue">foreach </span>(<span style="color: #2b91af">UserDefinedFunction </span>function <span style="color: blue">in </span>database.UserDefinedFunctions)
            {

                <span style="color: green">// Exclude system functions
                </span><span style="color: blue">if</span>(!function.IsSystemObject)
                {
                    <span style="color: green">// Generate script
                    // Include drop statements
                    </span><span style="color: #2b91af">StringBuilder </span>resultScript = <span style="color: blue">new </span><span style="color: #2b91af">StringBuilder</span>(<span style="color: blue">string</span>.Empty);

                    <span style="color: green">// Append drop statement
                    </span>resultScript.AppendFormat(<span style="color: #a31515">"IF  EXISTS (SELECT * FROM sys.objects WHERE object_id = OBJECT_ID(N'[dbo].[{0}]') AND type in (N'FN', N'IF', N'TF', N'FS', N'FT'))"</span>, function.Name).Append(<span style="color: #2b91af">Environment</span>.NewLine);
                    resultScript.AppendLine(<span style="color: #a31515">"BEGIN"</span>);
                    resultScript.AppendFormat(<span style="color: #a31515">"    DROP FUNCTION [dbo].[{0}]"</span>, function.Name).Append(<span style="color: #2b91af">Environment</span>.NewLine);
                    resultScript.AppendLine(<span style="color: #a31515">"END"</span>);
                    resultScript.AppendLine(<span style="color: #a31515">"GO"</span>);

                    <span style="color: green">// Add script to file content
                    </span><span style="color: blue">foreach </span>(<span style="color: blue">string </span>scriptLine <span style="color: blue">in </span>function.Script())
                    {
                        <span style="color: blue">string </span>line = scriptLine;
                        line = line.Replace(<span style="color: #a31515">"SET ANSI_NULLS ON"</span>, <span style="color: blue">string</span>.Empty);
                        line = line.Replace(<span style="color: #a31515">"SET QUOTED_IDENTIFIER ON"</span>, <span style="color: blue">string</span>.Empty);
                        line = line.Replace(<span style="color: #a31515">"SET ANSI_NULLS OFF"</span>, <span style="color: blue">string</span>.Empty);
                        line = line.Replace(<span style="color: #a31515">"SET QUOTED_IDENTIFIER OFF"</span>, <span style="color: blue">string</span>.Empty);
                        resultScript.AppendLine(line.Trim());
                    }

                    <span style="color: green">// Write file content to disk
                    </span><span style="color: blue">string </span>fileName = <span style="color: blue">string</span>.Format(<span style="color: #a31515">"{0}.sql"</span>, function.Name);
                    <span style="color: #2b91af">File</span>.WriteAllText(<span style="color: #2b91af">Path</span>.Combine(functionsOutputFolder.FullName, fileName), resultScript.ToString());
                }
            }
        }
    }
}

</pre><a href="http://11011.net/software/vspaste"></a><a href="http://11011.net/software/vspaste"></a><pre class="code">&nbsp;</pre><a href="http://11011.net/software/vspaste"></a><a href="http://11011.net/software/vspaste"></a>
<p>&nbsp;</p><a href="http://11011.net/software/vspaste"></a>
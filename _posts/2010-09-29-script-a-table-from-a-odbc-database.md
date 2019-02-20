---
ID: 1743
post_title: 'Script a table from a ODBC database with C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/09/29/script-a-table-from-a-odbc-database/
published: true
post_date: 2010-09-29 14:40:51
---
<p>If you want to create a corresponding SQL Server database table, from a ODBC table, you can use the following C# function:</p>  <p><strong>Note</strong></p>  <p>This function is not bullet proof, but gives you a simple example:</p>  <pre class="code">        <span style="color: blue">public void </span>ScriptODBCTable()
        {
            <span style="color: blue">string </span>outputFolderPath = <span style="color: #a31515">@&quot;C:\Temp&quot;</span>;
            <span style="color: blue">string </span>tableName = <span style="color: #a31515">&quot;MyTableName&quot;</span>;
            <span style="color: blue">string </span>fullTableName = <span style="color: #a31515">&quot;[dbo].[MyTableName]&quot;</span>;

            <span style="color: green">// Delete output folder if it exist
            </span><span style="color: #2b91af">DirectoryInfo </span>outputFolder = <span style="color: blue">new </span><span style="color: #2b91af">DirectoryInfo</span>(outputFolderPath);
            <span style="color: blue">if </span>(<span style="color: #2b91af">Directory</span>.Exists(outputFolder.FullName)) { <span style="color: #2b91af">Directory</span>.Delete(outputFolder.FullName, <span style="color: blue">true</span>); }

            <span style="color: green">// Create [Output] folder
            </span>outputFolder.Create();

            <span style="color: green">// Create [Tables] output folder
            </span><span style="color: #2b91af">DirectoryInfo </span>tablesOutputFolder = <span style="color: blue">new </span><span style="color: #2b91af">DirectoryInfo</span>(<span style="color: #2b91af">Path</span>.Combine(outputFolder.FullName, <span style="color: #a31515">&quot;Tables&quot;</span>));
            tablesOutputFolder.Create();

            <span style="color: green">// Generate script
            </span><span style="color: #2b91af">StringBuilder </span>resultScript = <span style="color: blue">new </span><span style="color: #2b91af">StringBuilder</span>(<span style="color: blue">string</span>.Empty);
            resultScript.AppendFormat(<span style="color: #a31515">&quot;IF NOT EXISTS (SELECT * FROM sys.objects WHERE object_id = OBJECT_ID(N'{0}') AND type in (N'U'))&quot;</span>, fullTableName).Append(<span style="color: #2b91af">Environment</span>.NewLine);
            resultScript.AppendLine(<span style="color: #a31515">&quot;BEGIN&quot;</span>);
            resultScript.Append(<span style="color: #a31515">&quot;CREATE TABLE &quot;</span>).Append(fullTableName).Append(<span style="color: #a31515">&quot; (&quot;</span>).Append(<span style="color: #2b91af">Environment</span>.NewLine);

            <span style="color: blue">using </span>(<span style="color: #2b91af">OdbcConnection </span>connection = <span style="color: blue">new </span><span style="color: #2b91af">OdbcConnection</span>(<span style="color: #a31515">&quot;uid=myUserName;Dsn=MySystemDnsName;pwd=MyPassword;&quot;</span>))
            {
                connection.Open();

                <span style="color: #2b91af">List</span>&lt;<span style="color: #2b91af">ScriptColumn</span>&gt; scriptColumns = <span style="color: blue">new </span><span style="color: #2b91af">List</span>&lt;<span style="color: #2b91af">ScriptColumn</span>&gt;();
                <span style="color: blue">using </span>(<span style="color: #2b91af">DataTable </span>table = connection.GetSchema(<span style="color: #a31515">&quot;Columns&quot;</span>))
                {
                    <span style="color: blue">int </span>i = 0;
                    <span style="color: blue">foreach </span>(<span style="color: #2b91af">DataRow </span>row <span style="color: blue">in </span>table.Rows)
                    {
                        <span style="color: blue">if </span>(i == 0)
                        {
                            <span style="color: blue">foreach </span>(System.Data.<span style="color: #2b91af">DataColumn </span>column <span style="color: blue">in </span>row.Table.Columns)
                            {
                                <span style="color: blue">string </span>name = column.ColumnName;
                                <span style="color: #2b91af">Console</span>.WriteLine(name);
                            }
                            i++;
                        }
                        <span style="color: blue">if </span>(row[<span style="color: #a31515">&quot;TABLE_NAME&quot;</span>].ToString().Equals(tableName))
                        {
                            scriptColumns.Add(<span style="color: blue">new </span><span style="color: #2b91af">ScriptColumn 
                            </span>{
                                Name = row[<span style="color: #a31515">&quot;COLUMN_NAME&quot;</span>].ToString(),
                                OrdinalPosition = (<span style="color: blue">int</span>)row[<span style="color: #a31515">&quot;ORDINAL_POSITION&quot;</span>],
                                ColumnSize = row[<span style="color: #a31515">&quot;COLUMN_SIZE&quot;</span>].ToString(),
                                Type = row[<span style="color: #a31515">&quot;TYPE_NAME&quot;</span>].ToString(),
                                Nullable = (row[<span style="color: #a31515">&quot;NULLABLE&quot;</span>].ToString().Equals(<span style="color: #a31515">&quot;1&quot;</span>)) ? <span style="color: #a31515">&quot;NULL&quot; </span>: <span style="color: #a31515">&quot;NOT NULL&quot;
                            </span>});
                        }
                    }
                }
                <span style="color: blue">var </span>sortedScriptColumns =
                    <span style="color: blue">from </span>sc <span style="color: blue">in </span>scriptColumns
                    <span style="color: blue">orderby </span>sc.OrdinalPosition
                    <span style="color: blue">select </span>sc;

                scriptColumns = sortedScriptColumns.ToList&lt;<span style="color: #2b91af">ScriptColumn</span>&gt;();

                <span style="color: blue">foreach </span>(<span style="color: #2b91af">ScriptColumn </span>column <span style="color: blue">in </span>scriptColumns)
                {
                    <span style="color: blue">if </span>(column.Type.Equals(<span style="color: #a31515">&quot;varchar&quot;</span>) || column.Type.Equals(<span style="color: #a31515">&quot;nvarchar&quot;</span>))
                    {
                        resultScript.AppendLine(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;[{0}] [{1}] ({2}) {3},&quot;</span>, column.Name, column.Type, column.ColumnSize, column.Nullable));
                    }
                    <span style="color: blue">else
                    </span>{
                        resultScript.AppendLine(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;[{0}] [{1}] {2},&quot;</span>, column.Name, column.Type, column.Nullable));
                    }
                }
            }

            <span style="color: green">// Remove ',' from last line
            </span><span style="color: blue">string </span>comma = <span style="color: #a31515">&quot;,&quot; </span>+ <span style="color: #2b91af">Environment</span>.NewLine;
            resultScript = <span style="color: blue">new </span><span style="color: #2b91af">StringBuilder</span>(resultScript.ToString().TrimEnd(comma.ToCharArray()));
            resultScript.Append(<span style="color: #2b91af">Environment</span>.NewLine);
            resultScript.AppendLine(<span style="color: #a31515">&quot;)&quot;</span>);
            resultScript.AppendLine(<span style="color: #a31515">&quot;END&quot;</span>);

            <span style="color: green">// Write file content to disk
            </span><span style="color: blue">string </span>fileName = <span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;{0}.sql&quot;</span>, fullTableName);
            <span style="color: #2b91af">File</span>.WriteAllText(<span style="color: #2b91af">Path</span>.Combine(tablesOutputFolder.FullName, fileName), resultScript.ToString());
        }
    }</pre>

<p>&#160;</p>

<pre class="code"><p><span style="color: blue">public class </span><span style="color: #2b91af">ScriptColumn
    </span>{
        <span style="color: blue">private string </span>_type;
        <span style="color: blue">public string </span>Name { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
        <span style="color: blue">public int </span>OrdinalPosition { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
        <span style="color: blue">public string </span>Type 
        {
            <span style="color: blue">get
            </span>{
                <span style="color: blue">return </span>_type;
            }
            <span style="color: blue">set
            </span>{
                _type = <span style="color: blue">value</span>;
                <span style="color: blue">if </span>(!<span style="color: blue">string</span>.IsNullOrEmpty(_type))
                {
                    <span style="color: blue">if </span>(_type.Equals(<span style="color: #a31515">&quot;integer&quot;</span>)) { _type = <span style="color: #a31515">&quot;int&quot;</span>; }
                    <span style="color: blue">if </span>(_type.Equals(<span style="color: #a31515">&quot;date&quot;</span>)) { _type = <span style="color: #a31515">&quot;datetime&quot;</span>; }</p><p><span style="color: blue">                    if </span>(_type.Equals(<span style="color: #a31515">&quot;varchar&quot;</span>)) { _type = <span style="color: #a31515">&quot;nvarchar&quot;</span>; }
                }
            }
        }
        <span style="color: blue">public string </span>ColumnSize { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
        <span style="color: blue">public string </span>Nullable { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
    }</p></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p>&#160;</p>

<p>&#160;</p>

<p><a href="http://11011.net/software/vspaste"></a></p>
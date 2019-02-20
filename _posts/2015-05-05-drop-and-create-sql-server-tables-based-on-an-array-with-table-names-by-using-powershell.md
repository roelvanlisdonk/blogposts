---
ID: 4328
post_title: >
  drop and create SQL Server tables based
  on an array with table names by using
  PowerShell
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/05/05/drop-and-create-sql-server-tables-based-on-an-array-with-table-names-by-using-powershell/
published: true
post_date: 2015-05-05 12:25:55
---
<p>&#160;</p>  <pre class="code"><span style="background: white; color: #006400"># Add table names to the &quot;$tables&quot; array in the order they should be created.
</span><span style="background: white; color: #ff4500">$tables </span><span style="background: white; color: #a9a9a9">= </span><span style="background: white; color: black">@(
    </span><span style="background: white; color: darkred">&quot;dbo.Person&quot;</span><span style="background: white; color: #a9a9a9">,
    </span><span style="background: white; color: darkred">&quot;dbo.Settings&quot;</span><span style="background: white; color: #a9a9a9">,
    </span><span style="background: white; color: darkred">&quot;dbo.SmsStatus&quot;</span><span style="background: white; color: #a9a9a9">,
    </span><span style="background: white; color: darkred">&quot;dbo.Sms&quot;
</span><span style="background: white; color: black">)

</span><span style="background: white; color: #006400"># Create a table if it does not exist.
# It expects the &quot;create scripts&quot; to be located in a subfolder &quot;Tables&quot;.
</span><span style="background: white; color: #00008b">function </span><span style="background: white; color: #8a2be2">CreateTable
</span><span style="background: white; color: black">{
    </span><span style="background: white; color: #a9a9a9">[</span><span style="background: white; color: teal">string</span><span style="background: white; color: #a9a9a9">]</span><span style="background: white; color: #ff4500">$table </span><span style="background: white; color: #a9a9a9">= </span><span style="background: white; color: #ff4500">$args</span><span style="background: white; color: #a9a9a9">[</span><span style="background: white; color: purple">0</span><span style="background: white; color: #a9a9a9">]
    [</span><span style="background: white; color: teal">string</span><span style="background: white; color: #a9a9a9">]</span><span style="background: white; color: #ff4500">$file </span><span style="background: white; color: #a9a9a9">= </span><span style="background: white; color: darkred">&quot;{0}\Tables\{1}.sql&quot; </span><span style="background: white; color: #a9a9a9">-f </span><span style="background: white; color: #ff4500">$PSScriptRoot</span><span style="background: white; color: #a9a9a9">, </span><span style="background: white; color: #ff4500">$table
    </span><span style="background: white; color: blue">Echo</span><span style="background: white; color: black">(</span><span style="background: white; color: darkred">&quot;create table {0}&quot; </span><span style="background: white; color: #a9a9a9">-f </span><span style="background: white; color: #ff4500">$table</span><span style="background: white; color: black">) 
    </span><span style="background: white; color: blue">Invoke-Sqlcmd </span><span style="background: white; color: navy">-ServerInstance </span><span style="background: white; color: darkred">&quot;(localdb)\v11.0&quot; </span><span style="background: white; color: navy">-Database </span><span style="background: white; color: darkred">&quot;MyDatabase&quot; </span><span style="background: white; color: navy">-InputFile </span><span style="background: white; color: #ff4500">$file
</span><span style="background: white; color: black">}

</span><span style="background: white; color: #006400"># Drop a table if it exists.
</span><span style="background: white; color: #00008b">function </span><span style="background: white; color: #8a2be2">DropTable
</span><span style="background: white; color: black">{
    </span><span style="background: white; color: #a9a9a9">[</span><span style="background: white; color: teal">string</span><span style="background: white; color: #a9a9a9">]</span><span style="background: white; color: #ff4500">$table </span><span style="background: white; color: #a9a9a9">= </span><span style="background: white; color: #ff4500">$args</span><span style="background: white; color: #a9a9a9">[</span><span style="background: white; color: purple">0</span><span style="background: white; color: #a9a9a9">]
    [</span><span style="background: white; color: teal">string</span><span style="background: white; color: #a9a9a9">]</span><span style="background: white; color: #ff4500">$query </span><span style="background: white; color: #a9a9a9">= </span><span style="background: white; color: darkred">&quot;if object_id('{0}') is not null begin drop table {0} end&quot; </span><span style="background: white; color: #a9a9a9">-f </span><span style="background: white; color: #ff4500">$table
    </span><span style="background: white; color: blue">Echo</span><span style="background: white; color: black">(</span><span style="background: white; color: darkred">&quot;drop table {0}&quot; </span><span style="background: white; color: #a9a9a9">-f </span><span style="background: white; color: #ff4500">$table</span><span style="background: white; color: black">) 
    </span><span style="background: white; color: blue">Invoke-Sqlcmd </span><span style="background: white; color: navy">-ServerInstance </span><span style="background: white; color: darkred">&quot;(localdb)\v11.0&quot; </span><span style="background: white; color: navy">-Database </span><span style="background: white; color: darkred">&quot;MyDatabase&quot; </span><span style="background: white; color: navy">-Query </span><span style="background: white; color: #ff4500">$query
</span><span style="background: white; color: black">}

</span><span style="background: white; color: #00008b">function </span><span style="background: white; color: #8a2be2">DropTables
</span><span style="background: white; color: black">{
    </span><span style="background: white; color: #ff4500">$reverseTable </span><span style="background: white; color: #a9a9a9">= </span><span style="background: white; color: #ff4500">$tables</span><span style="background: white; color: #a9a9a9">.</span><span style="background: white; color: black">Clone()
    </span><span style="background: white; color: #a9a9a9">[</span><span style="background: white; color: teal">array</span><span style="background: white; color: #a9a9a9">]::</span><span style="background: white; color: black">Reverse(</span><span style="background: white; color: #ff4500">$reverseTable</span><span style="background: white; color: black">)
    </span><span style="background: white; color: #00008b">foreach </span><span style="background: white; color: black">(</span><span style="background: white; color: #ff4500">$table </span><span style="background: white; color: #00008b">in </span><span style="background: white; color: #ff4500">$reverseTable</span><span style="background: white; color: black">) {
       </span><span style="background: white; color: blue">DropTable </span><span style="background: white; color: #ff4500">$table
    </span><span style="background: white; color: black">}    
}

</span><span style="background: white; color: #00008b">function </span><span style="background: white; color: #8a2be2">CreateTables </span><span style="background: white; color: black">{
    </span><span style="background: white; color: #00008b">foreach </span><span style="background: white; color: black">(</span><span style="background: white; color: #ff4500">$table </span><span style="background: white; color: #00008b">in </span><span style="background: white; color: #ff4500">$tables</span><span style="background: white; color: black">) {
       </span><span style="background: white; color: blue">CreateTable </span><span style="background: white; color: #ff4500">$table
    </span><span style="background: white; color: black">}
}

</span><span style="background: white; color: blue">DropTables
CreateTables
</span></pre>


<p>Will drop all tables in $tables if they exist and then will create all tables in $tables if they do not exist.</p>
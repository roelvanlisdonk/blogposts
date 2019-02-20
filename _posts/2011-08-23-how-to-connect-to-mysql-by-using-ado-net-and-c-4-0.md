---
ID: 2133
post_title: 'How to connect to MySQL by using ADO .NET and C# 4.0'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/08/23/how-to-connect-to-mysql-by-using-ado-net-and-c-4-0/
published: true
post_date: 2011-08-23 13:47:01
---
<p align="left">Download the MySQL drivers at: <a title="http://dev.mysql.com/downloads/connector/net/" href="http://dev.mysql.com/downloads/connector/net/">http://dev.mysql.com/downloads/connector/net/</a></p>  <p align="left">Install the drivers on you’re development machine.</p>  <p align="left">&#160;</p>  <p align="left">At references to:</p>  <p align="left">- System.Data</p>  <p align="left">- MySql.Data [C:\Program Files (x86)\MySQL\MySQL Connector Net 6.4.3\Assemblies\v4.0\MySql.Data.dll]</p>  <p align="left">&#160;</p>  <p align="left">The following code will output all database names to the console window:</p>  <pre class="code"><span style="color: blue">using </span>System.Data;
<span style="color: blue">using </span>MySql.Data.MySqlClient;</pre>


<pre class="code"><span style="color: blue">string </span>connectionString = <span style="color: #2b91af">String</span>.Format(<span style="color: #a31515">&quot;Server=</span><span style="color: #3cb371">{0}</span><span style="color: #a31515">;Port=</span><span style="color: #3cb371">{1}</span><span style="color: #a31515">;Database=</span><span style="color: #3cb371">{2}</span><span style="color: #a31515">;Uid=</span><span style="color: #3cb371">{3}</span><span style="color: #a31515">;Pwd=</span><span style="color: #3cb371">{4}</span><span style="color: #a31515">;&quot;</span>,<br /> <span style="color: #a31515">&quot;192.168.1.1&quot;</span>, <span style="color: #a31515">&quot;3306&quot;</span>, <span style="color: #a31515">&quot;MyDatabaseName1&quot;</span>, <span style="color: #a31515">&quot;MyUserName1&quot;</span>, <span style="color: #a31515">&quot;MyPassword1&quot;</span>);

<span style="color: blue">using </span>(<span style="color: #2b91af">MySqlConnection </span>connection = <span style="color: blue">new </span><span style="color: #2b91af">MySqlConnection</span>(connectionString))
{
    <span style="color: blue">using </span>(<span style="color: #2b91af">MySqlCommand </span>cmd = <span style="color: blue">new </span><span style="color: #2b91af">MySqlCommand</span>(<span style="color: #a31515">&quot;SHOW DATABASES&quot;</span>, connection))
    {
        connection.Open();

        <span style="color: #2b91af">MySqlDataReader </span>reader = cmd.ExecuteReader();

        <span style="color: blue">while </span>(reader.Read())
        {
            <span style="color: #2b91af">Console</span>.WriteLine(reader.GetString(0));
        }
    }
}</pre>
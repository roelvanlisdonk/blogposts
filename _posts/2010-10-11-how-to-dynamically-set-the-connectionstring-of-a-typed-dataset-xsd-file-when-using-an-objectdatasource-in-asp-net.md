---
ID: 1746
post_title: 'How to dynamically set the connectionstring of a typed dataset (*.xsd file) when using an ObjectDataSource in ASP .NET'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/10/11/how-to-dynamically-set-the-connectionstring-of-a-typed-dataset-xsd-file-when-using-an-objectdatasource-in-asp-net/
published: true
post_date: 2010-10-11 16:47:15
---
<p align="left">If you are using a typed dataset (*.xsd) and you want to set it’s connection string, you can use the ObjectDataSource event OnObjectCreated.</p>  <p align="left">&#160;</p>  <pre class="code"><span style="color: blue">protected void </span>MyObjectDaDataSource_OnObjectCreated(<span style="color: blue">object </span>sender, <span style="color: #2b91af">ObjectDataSourceEventArgs </span>e)
{
    <span style="color: blue">if </span>(e != <span style="color: blue">null </span>&amp;&amp; e.ObjectInstance != <span style="color: blue">null</span>)
    {
        <span style="color: #2b91af">SqlConnection </span>connection = <span style="color: blue">new </span><span style="color: #2b91af">SqlConnection</span>(&quot;Data Source=SQLServerInstanceName1;<br />User ID=User1;Password=Password1;Initial Catalog=Database1;&quot;);
        e.ObjectInstance.GetType().GetProperty(<span style="color: #a31515">&quot;Connection&quot;</span>, <br /><span style="color: #2b91af">BindingFlags</span>.NonPublic | <span style="color: #2b91af">BindingFlags</span>.Instance).SetValue(e.ObjectInstance, connection, <span style="color: blue">null</span>);
    }
}</pre>
<a href="http://11011.net/software/vspaste"></a>
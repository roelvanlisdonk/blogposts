---
ID: 1070
post_title: >
  Get only the changed data from the
  database with Linq to SQL and .NET RIA
  Services in Silverlight 3
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/08/get-only-the-changed-data-from-the-database-with-linq-to-sql-and-net-ria-services-in-silverlight-3/
published: true
post_date: 2010-03-08 10:33:02
---
<p>If you cache data in you’re Silverlight 3 application and want to sync (get the latest data from the database) the entities, you can use the Load function with the LoadBehavior.RefreshCurrent option. This will get the latest data from the database, but only the changed entities. </p>  <pre class="code"><span style="color: blue">private </span><span style="color: #2b91af">EntitySet</span>&lt;<span style="color: #2b91af">TTUser</span>&gt; _userData;
        <span style="color: blue">public </span><span style="color: #2b91af">EntitySet</span>&lt;<span style="color: #2b91af">TTUser</span>&gt; UserData
        {
            <span style="color: blue">get
            </span>{
                <span style="color: blue">return </span>_userData;
            }
            <span style="color: blue">set
            </span>{
                _userData = <span style="color: blue">value</span>;
            }
        }</pre>
<a href="http://11011.net/software/vspaste"></a>

<pre class="code"><span style="color: blue"></span></pre>

<pre class="code"><span style="color: blue">private void </span>Button_Click(<span style="color: blue">object </span>sender, System.Windows.<span style="color: #2b91af">RoutedEventArgs </span>e)
        {
            <span style="color: blue">if </span>(<span style="color: #2b91af">WebContext</span>.Current.User.IsAuthenticated)
            {
                <span style="color: #2b91af">TTSDomainContext </span>context = <span style="color: blue">new </span><span style="color: #2b91af">TTSDomainContext</span>();
                <span style="color: blue">this</span>.UserData = context.TTUsers;
                tasksDataGrid.ItemsSource = <span style="color: blue">this</span>.UserData;
                context.Load(context.GetUsersQuery(),<span style="color: #2b91af">LoadBehavior</span>.RefreshCurrent,<span style="color: blue">true</span>);
            }
        }</pre>

<p>&#160;</p>

<p>You can use the Submitchanges() function to update the database.</p>
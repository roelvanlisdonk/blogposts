---
ID: 858
post_title: >
  Delete all records from a table with
  LLBLGen Pro v2.6
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/12/18/delete-all-records-from-a-table-with-llblgen-pro-v2-6/
published: true
post_date: 2009-12-18 13:58:05
---
<p>If you want to delete all records from a table with LLBLGen Pro v2.6 without first fetching all records, you can use the DataAccessAdapter DeleteEntitiesDirectly function.</p>  <pre class="code"><span style="color: green">            // Define the query that matches all records to be deleted.<br />            // If no PredicateExpression are added all records will be deleted.
            </span><span style="color: #2b91af">RelationPredicateBucket </span>bucket = <span style="color: blue">new </span><span style="color: #2b91af">RelationPredicateBucket</span>();

            <span style="color: green">// If you want to delete only the customers that have an Id != 100, uncomment the following line
            // bucket.PredicateExpression.Add(CustomerFields.Id != 100);

            // Initialize DataAccessAdapter
            </span><span style="color: blue">using </span>(<span style="color: #2b91af">DataAccessAdapter </span>da = <span style="color: blue">new </span><span style="color: #2b91af">DataAccessAdapter</span>(<span style="color: #a31515">&quot;server=MyServer; database=Test; Trusted_Connection=False;&quot;</span>))
            {
                <span style="color: green">// Delete the records from table CustomerEntity (TSQL query: delete Customer)
                </span>da.DeleteEntitiesDirectly(<span style="color: #a31515">&quot;CustomerEntity&quot;</span>, bucket);
            }</pre>
<a href="http://11011.net/software/vspaste"></a><a href="http://11011.net/software/vspaste"></a>
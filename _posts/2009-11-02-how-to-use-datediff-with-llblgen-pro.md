---
ID: 792
post_title: How to use datediff with LLBLGen Pro
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/11/02/how-to-use-datediff-with-llblgen-pro/
published: true
post_date: 2009-11-02 16:36:49
---
<p>If you want to use datedif to filter on a date, you can use code like:   <br /></p>  <pre class="code"><span style="color: blue">        public </span><span style="color: #2b91af">EntityCollection</span>&lt;<span style="color: #2b91af">Customers</span>&gt; GetCustomers(<span style="color: #2b91af">DateTime </span>creationDate)
        {
            <span style="color: #2b91af">EntityCollection</span>&lt;<span style="color: #2b91af">AfhaalopdrachtEntity</span>&gt; result = <span style="color: blue">new </span><span style="color: #2b91af">EntityCollection</span>&lt;<span style="color: #2b91af">AfhaalopdrachtEntity</span>&gt;();

            <span style="color: green">// Filter
            </span><span style="color: #2b91af">IRelationPredicateBucket </span>filter = <span style="color: blue">new </span><span style="color: #2b91af">RelationPredicateBucket</span>();

            <span style="color: #2b91af">IPredicate </span>customerCreateDateFilter = <span style="color: blue">new </span><span style="color: #2b91af">EntityField2</span>(<span style="color: #a31515">&quot;CreateCustomerDiff&quot;</span>, <span style="color: blue">new </span><span style="color: #2b91af">DbFunctionCall</span>(<span style="color: #a31515">&quot;DATEDIFF(day, {0}, {1})&quot;</span>, <span style="color: blue">new object</span>[] { <span style="color: #2b91af">CustomerFields</span>.CreationDate, creationDate})) == 0;
            filter.PredicateExpression.Add(customerCreateDateFilter );

            <span style="color: green">// Fetch (get the data)
            </span><span style="color: blue">using </span>(<span style="color: #2b91af">DataAccessAdapter </span>da = <span style="color: #2b91af">ConnectionHelper</span>.GetAdapter(<span style="color: #2b91af">Source</span>.Pegaso, <span style="color: #2b91af">Global</span>.Logger))
            {
                da.FetchEntityCollection(result, filter);
            }

           <span style="color: blue">return </span>result;
        }</pre>
<a href="http://11011.net/software/vspaste"></a>
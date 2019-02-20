---
ID: 413
post_title: >
  Sort ASP .NET Gridview on related table
  (prefetchpath) column with LLBLGen Pro
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/19/sort-asp-net-gridview-on-related-table-prefetchpath-column-with-llblgen-pro/
published: true
post_date: 2009-05-19 17:07:12
---
<p>If you have a table Order and a related table Customer, you can sort and filter this data for ASP .NET with LLBLGen pro, as mentioned in the LLBLGen Pro documentation:</p>  <p>// Define result entitycollection   <br />EntityCollection&lt;CustomerEntity&gt; customers = new EntityCollection&lt;CustomerEntity&gt;();    <br />    <br />// Define sort (sort result on column &quot;Order.ShipCountry&quot;)    <br />SortExpression result = new SortExpression();    <br />result.Add(CustomerFields.Name | SortOperator.Ascending);    <br />result[0].CaseSensitiveCollation = false;    <br />    <br />// Define filter by adding relations (= inner join in tsql)    <br />RelationPredicateBucket customerFilter = new RelationPredicateBucket();     <br />customerFilter.Relations.Add(CustomerEntity.Relations.OrderEntityUsingCustomerId);     <br />    <br />// Define filter by adding predicateexpression (= where in tsql)    <br />customerFilter.PredicateExpression.Add(OrderFields.ShipCountry==&quot;Brazil&quot;);     <br />    <br />// Load for all customers fetched their orders.     <br />PrefetchPath2 path = new PrefetchPath2(EntityType.CustomerEntity);     <br />path.Add(CustomerEntity.PrefetchPathOrders);    <br />    <br />// Get the data    <br />using(DataAccessAdapter adapter = new DataAccessAdapter())     <br />{     <br />&#160;&#160;&#160;&#160; adapter.FetchEntityCollection(customers, customerFilter, path);     <br />}    <br />    <br />If you forget to add the relations, you might get the exception:    <br />    <br />An exception was caught during the execution of a retrieval query: The multi-part identifier &quot;dbo.Customer.Name&quot; could not be bound.. Check InnerException, QueryExecuted and Parameters of this exception to examine the cause of this exception.    <br />    <br />This is because there is no inner join on Customer, so Customer.Name does not exist in the query</p>
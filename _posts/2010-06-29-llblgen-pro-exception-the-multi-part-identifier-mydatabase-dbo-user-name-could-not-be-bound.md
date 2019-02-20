---
ID: 1575
post_title: 'LLBLGen Pro exception: The multi-part identifier &quot;MyDatabase.dbo.User.Name&quot; could not be bound'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/06/29/llblgen-pro-exception-the-multi-part-identifier-mydatabase-dbo-user-name-could-not-be-bound/
published: true
post_date: 2010-06-29 11:16:27
---
<p>If you get an exception like:</p>  <p align="left">System.Web.HttpUnhandledException (0x80004005): Exception of type 'System.Web.HttpUnhandledException' was thrown. ---&gt; SD.LLBLGen.Pro.ORMSupportClasses.ORMQueryExecutionException: An exception was caught during the execution of a retrieval query: The multi-part identifier &quot;MyDatabase.dbo.User.Name&quot; could not be bound..</p>  <p align="left">make sure you use corresponding EntityFactory and Fields: </p>  <p>&#160;</p>  <pre class="code"><p><span style="color: #2b91af">EntityCollection </span>items = <span style="color: blue">new </span><span style="color: #2b91af">EntityCollection</span>(<span style="color: blue">new </span><span style="color: #2b91af"><strong><em>UserEntityFactory</em></strong></span>());
<span style="color: #2b91af">PredicateExpression </span>filter = <span style="color: blue">new </span><span style="color: #2b91af">PredicateExpression</span>(<span style="color: #2b91af"><strong><em>Userields</em></strong></span>.Name == username);
<span style="color: #2b91af">IRelationPredicateBucket </span>bucket = <span style="color: blue">new </span><span style="color: #2b91af">RelationPredicateBucket</span>();
bucket.PredicateExpression.AddWithAnd(filter);

<span style="color: blue">using </span>(<span style="color: blue">var </span>adapter = <span style="color: #2b91af">ConnectionHelper</span>.GetAdapter(<span style="color: #2b91af">Source</span>.LocatiePlatform, _logger))
{&#160;&#160;&#160;&#160; adapter.FetchEntityCollection(items, bucket);&#160;&#160;&#160;&#160; adapter.CloseConnection();
}
</p><p>&#160;</p><p>&#160;</p></pre>
In the code above if you change the UserEntityFactory to an other “table factory” like PersonEntityFactory, you will get the 0x80004005 exception.
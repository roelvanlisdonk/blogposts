---
ID: 366
post_title: 'Error on calling stored procedure with LLBLGen Pro {&quot;The ConnectionString property has not been initialized.&quot;}'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/07/error-on-calling-stored-procedure-with-llblgen-pro-the-connectionstring-property-has-not-been-initialized/
published: true
post_date: 2009-05-07 08:50:15
---
<p>When you get the error {"The ConnectionString property has not been initialized."} on calling a stored procedure with LLBLGen Pro, you probably forgot to set the parameter "DataAccessAdapter adapter" on you're LLBLGen Pro methode call:<br /><br />RetrievalProcedures.MyStoreProcedure(param1, param2, dataAccessAdapter);<br /></p> <p>if you call the function like RetrievalProcedures.MyStoreProcedure(param1, param2); you will get the error {"The ConnectionString property has not been initialized."} </p>
---
ID: 1455
post_title: >
  Exception during SaveEntity with LLBLGen
  Pro
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/06/15/exception-during-saveentity-with-llblgen-pro/
published: true
post_date: 2010-06-15 13:23:51
---
<p align="left">I wanted to update an entity with LLGLGen Pro by executing the adapter.SaveEntity() method and got an exception. </p>  <p align="left">&#160;</p>  <p align="left"><strong>Error</strong></p>  <p align="left">An exception was caught during the execution of an action query: Cannot insert duplicate key row in object 'dbo.Customer' with unique index 'UniqueApi'.   <br />The statement has been terminated.. Check InnerException, QueryExecuted and Parameters of this exception to examine the cause of this exception.</p>  <p align="left">&#160;</p>  <p align="left"><strong>Cause</strong></p>  <p align="left">This was caused by an unique constraint on a column ApiKey, but I was updating an existing “Customer” entity and the value for the “ApiKey”, was unique, but I forgot to set the IsNew property on the “Customer” entity to false. So LLGLGen wanted to insert a new record instead of updating the existing record.</p>  <p align="left">&#160;</p>  <p align="left"><strong>Solution</strong></p>  <p align="left">By setting the “IsNew” property on the “Customer” entity to false, the exception was resolved.</p>
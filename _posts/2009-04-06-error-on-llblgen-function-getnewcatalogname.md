---
ID: 321
post_title: >
  Error on LLBLGen function
  GetNewCatalogName
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/04/06/error-on-llblgen-function-getnewcatalogname/
published: true
post_date: 2009-04-06 11:02:46
---
<p>If you don't set the property CatalogNameToUse in class DataAccessAdapter correctly, using the DataAccessAdapter can result in an error:</p> <p>System.NullReferenceException : Object reference not set to an instance of an object.<br />&nbsp;&nbsp;&nbsp; at SD.LLBLGen.Pro.DQE.SqlServer.DynamicQueryEngine.GetNewCatalogName(String currentName)</p>Change the name to the correct "Database Name" solved the problem
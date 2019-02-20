---
ID: 2495
post_title: How to do unit testing with EF 4.2
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/02/08/how-to-do-unit-testing-with-ef-4-2/
published: true
post_date: 2012-02-08 16:24:46
---
<p align="left">If you want to do unit testing with Entity Framework 4.2, I suggest you read this article: <a href="http://romiller.com/2010/09/07/ef-ctp4-tips-tricks-testing-with-fake-dbcontext/">http://romiller.com/2010/09/07/ef-ctp4-tips-tricks-testing-with-fake-dbcontext/</a></p>  <p align="left">It explains how to create a Interface for you DbContext and create fake implementations for the IDbSet, so you can stub your database.</p>
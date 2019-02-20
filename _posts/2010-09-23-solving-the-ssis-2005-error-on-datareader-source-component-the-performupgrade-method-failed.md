---
ID: 1735
post_title: 'Solving the SSIS 2005 error on DataReader Source component: The PerformUpgrade method failed'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/09/23/solving-the-ssis-2005-error-on-datareader-source-component-the-performupgrade-method-failed/
published: true
post_date: 2010-09-23 12:01:50
---
<p>&#160;</p>  <p>I create a new VMWare development image and got the following error:</p>  <p>Error loading TestPackage.dtsx: The component metadata for &quot;component &quot;SRC_TestTable&quot; (1)&quot; could not be upgraded to the newer version of the component. The PerformUpgrade method failed.</p>  <p>&#160;</p>  <p>When opening the SSIS 2005 package in Microsoft SQL Server Business Intelligence Development Studio 2005.</p>  <p>I solved the error by installing the latest Service Packs on the new development image.</p>
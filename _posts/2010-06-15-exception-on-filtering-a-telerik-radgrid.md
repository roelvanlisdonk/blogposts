---
ID: 1456
post_title: Exception on filtering a telerik RadGrid
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/06/15/exception-on-filtering-a-telerik-radgrid/
published: true
post_date: 2010-06-15 14:36:23
---
<p align="left">I was getting an error when I filtered a telerik RadGrid:</p>  <p align="left">&#160;</p>  <p align="left"><strong>Error</strong></p>  <p align="left">System.Web.HttpUnhandledException (0x80004005): Exception of type 'System.Web.HttpUnhandledException' was thrown. ---&gt; No property or field 'Name' exists in type 'EntityBase2' (at index 5) at System.Web.UI.Page.HandleError(Exception e) at System.Web.UI.Page.ProcessRequestMain(Boolean includeStagesBeforeAsyncPoint, Boolean includeStagesAfterAsyncPoint) at System.Web.UI.Page.ProcessRequest(Boolean includeStagesBeforeAsyncPoint, Boolean includeStagesAfterAsyncPoint) at System.Web.UI.Page.ProcessRequest() at System.Web.UI.Page.ProcessRequestWithNoAssert(HttpContext context) at System.Web.UI.Page.ProcessRequest(HttpContext context) at ASP.customeroverview_aspx.ProcessRequest(HttpContext context) in c:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\dd255f7a\3799692b\App_Web_1qm10fjh.0.cs:line 0 at System.Web.HttpApplication.CallHandlerExecutionStep.System.Web.HttpApplication.IExecutionStep.Execute() at System.Web.HttpApplication.ExecuteStep(IExecutionStep step, Boolean&amp; completedSynchronously)</p>  <p align="left">&#160;</p>  <p align="left"><strong>Solution</strong></p> After setting the RadGrid property “EnableLinqExpression” to false, the exception was resolved and I could filter my telerik RadGrid&#160; <pre class="code"><span style="color: red">EnableLinqExpressions</span><span style="color: blue">=&quot;false&quot;
</span></pre>
<a href="http://11011.net/software/vspaste"></a>
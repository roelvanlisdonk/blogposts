---
ID: 565
post_title: >
  How to use the ReportViewer.Drillthrough
  event in ASP .NET 2.0
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/06/22/how-to-use-the-reportviewerdrillthrough-event-in-asp-net-20/
published: true
post_date: 2009-06-22 09:52:14
---
<p>If you have created a Microsoft Reporting Server report with a drillthrough. The user can Navigate to another report by clicking a link. This will fire the ReportViewer.Drilltrhough event on a ReportViewer control in ASP .NET 2.0. The DrillthroughEventArgs contains the new ReportPath. With this information you can create navigate to the correct URL on you’re ASP .NET 2.0 website.   <br />    <br /></p>  <pre class="code"><span style="color: blue">        protected void </span>ReportViewer1_Drillthrough(<span style="color: blue">object </span>sender, Microsoft.Reporting.WebForms.<span style="color: #2b91af">DrillthroughEventArgs </span>e)
        {
            Response.Redirect(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;Test.aspx?reportPath={0}&quot;</span>, e.ReportPath));
        }</pre>
<a href="http://11011.net/software/vspaste"></a>
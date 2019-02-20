---
ID: 572
post_title: >
  Add a WebService reference to a
  Microsoft Office Excel sheet
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/06/24/add-a-webservice-reference-to-a-microsoft-office-excel-sheet/
published: true
post_date: 2009-06-24 10:16:12
---
<p>&gt; Start you’re webservice    <br />&gt; Start Microsoft Office Excel     <br />&gt; Show the Control Toolbox toolbar: &gt; View &gt; Toolbars &gt; Control Toolbox     <br />&gt; Enter Design mode by clicking the “Design Mode” button on the Control Toolbox     <br />&gt; Add a button to you’re Excel sheet     <br />&gt; Double click the button, this will op en de Microsoft Visual Basic Editor     <br />&gt; In the Microsoft Visual Basic Editor click: Tools &gt; Web Service Reference… &gt;     <br />&gt; On the Microsoft Office 2003 Web Services Toolkit dialog click: “Web Service URL” and enter you’re Web Service URL, click Search     <br />&gt; In the Search Results area, check you’re Web Service and click Add     <br />    <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/06/image7.png"><img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/06/image-thumb7.png" width="607" height="386" /></a>     <br />    <br />This will generate a class “clsws_Service” with methods foreach WebMethod of the WebService, but the constant “Private c_WSDL_URL As String” should be changed to “Public URL As String”, so you can set the URL dynamic like:     <br /></p>  <p>&#160;&#160;&#160; Dim service As New clsws_Service    <br />&#160;&#160;&#160; Dim data As String     <br />&#160;&#160;&#160; <strong>service.URL</strong> = ActiveSheet.Cells(1, &quot;A&quot;).Value     <br />&#160;&#160;&#160; data = service.wsm_GetOpsMail(ActiveSheet.Cells(2, &quot;A&quot;).Value, ActiveSheet.Cells(3, &quot;A&quot;).Value)    <br />    <br />More information can be found on: <a title="http://www.brainbell.com/tutorials/ms-office/excel/Access_SOAP_Web_Services_From_Excel.htm" href="http://www.brainbell.com/tutorials/ms-office/excel/Access_SOAP_Web_Services_From_Excel.htm">http://www.brainbell.com/tutorials/ms-office/excel/Access_SOAP_Web_Services_From_Excel.htm</a></p>
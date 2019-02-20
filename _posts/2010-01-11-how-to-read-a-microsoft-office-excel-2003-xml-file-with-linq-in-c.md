---
ID: 924
post_title: 'How to read a Microsoft Office Excel 2003 xml file with LINQ in C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/01/11/how-to-read-a-microsoft-office-excel-2003-xml-file-with-linq-in-c/
published: true
post_date: 2010-01-11 10:51:30
---
<p>If you want to read a specific cell from a Microsoft Office Excel file (*.xml) with LINQ in C# you can use the following code:   <br />    <br /><strong>Microsoft Office Excel 2003 file (“C:\BDATA\Cars.xml”) with a worksheet “Settings”:     <br /></strong><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image2.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb2.png" width="244" height="235" /></a>     <br />    <br />Code to read the value “Leon”</p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Text;
<span style="color: blue">using </span>NUnit.Framework;
<span style="color: blue">using </span>System.Xml.Linq;

<span style="color: blue">namespace </span>UnitTest
{
    [<span style="color: #2b91af">TestFixture</span>]
    <span style="color: blue">public class </span><span style="color: #2b91af">TestCode
    </span>{
        [<span style="color: #2b91af">Test</span>]
        <span style="color: blue">public void </span>ReadExcelCellTest()
        {
            <span style="color: #2b91af">XDocument </span>document = <span style="color: #2b91af">XDocument</span>.Load(<span style="color: #a31515">@&quot;C:\BDATA\Cars.xml&quot;</span>);
            <span style="color: #2b91af">XNamespace </span>workbookNameSpace = <span style="color: #a31515">@&quot;urn:schemas-microsoft-com:office:spreadsheet&quot;</span>;

            <span style="color: green">// Get worksheet
            </span><span style="color: blue">var </span>query = <span style="color: blue">from </span>w <span style="color: blue">in </span>document.Elements(workbookNameSpace + <span style="color: #a31515">&quot;Workbook&quot;</span>).Elements(workbookNameSpace + <span style="color: #a31515">&quot;Worksheet&quot;</span>)
                        <span style="color: blue">where </span>w.Attribute(workbookNameSpace + <span style="color: #a31515">&quot;Name&quot;</span>).Value.Equals(<span style="color: #a31515">&quot;Settings&quot;</span>)
                        <span style="color: blue">select </span>w;
            <span style="color: #2b91af">List</span>&lt;<span style="color: #2b91af">XElement</span>&gt; foundWoksheets = query.ToList&lt;<span style="color: #2b91af">XElement</span>&gt;();
            <span style="color: blue">if </span>(foundWoksheets.Count() &lt;= 0) { <span style="color: blue">throw new </span><span style="color: #2b91af">ApplicationException</span>(<span style="color: #a31515">&quot;Worksheet Settings could not be found&quot;</span>); }
            <span style="color: #2b91af">XElement </span>worksheet = query.ToList&lt;<span style="color: #2b91af">XElement</span>&gt;()[0];

            <span style="color: green">// Get the row for &quot;Seat&quot;
            </span>query = <span style="color: blue">from </span>d <span style="color: blue">in </span>worksheet.Elements(workbookNameSpace + <span style="color: #a31515">&quot;Table&quot;</span>).Elements(workbookNameSpace + <span style="color: #a31515">&quot;Row&quot;</span>).Elements(workbookNameSpace + <span style="color: #a31515">&quot;Cell&quot;</span>).Elements(workbookNameSpace + <span style="color: #a31515">&quot;Data&quot;</span>)
                    <span style="color: blue">where </span>d.Value.Equals(<span style="color: #a31515">&quot;Seat&quot;</span>)
                    <span style="color: blue">select </span>d;
            <span style="color: #2b91af">List</span>&lt;<span style="color: #2b91af">XElement</span>&gt; foundData = query.ToList&lt;<span style="color: #2b91af">XElement</span>&gt;();
            <span style="color: blue">if </span>(foundData.Count() &lt;= 0) { <span style="color: blue">throw new </span><span style="color: #2b91af">ApplicationException</span>(<span style="color: #a31515">&quot;Row 'Seat' could not be found&quot;</span>); }
            <span style="color: #2b91af">XElement </span>row = query.ToList&lt;<span style="color: #2b91af">XElement</span>&gt;()[0].Parent.Parent;

            <span style="color: green">// Get value cell of Etl_SPIImportLocation_ImportPath setting
            </span><span style="color: #2b91af">XElement </span>cell = row.Elements().ToList&lt;<span style="color: #2b91af">XElement</span>&gt;()[1];

            <span style="color: green">// Get the value &quot;Leon&quot;
            </span><span style="color: blue">string </span>cellValue = cell.Elements(workbookNameSpace + <span style="color: #a31515">&quot;Data&quot;</span>).ToList&lt;<span style="color: #2b91af">XElement</span>&gt;()[0].Value;

            <span style="color: #2b91af">Console</span>.WriteLine(cellValue);
        }
    }
}</pre>
<a href="http://11011.net/software/vspaste"></a>
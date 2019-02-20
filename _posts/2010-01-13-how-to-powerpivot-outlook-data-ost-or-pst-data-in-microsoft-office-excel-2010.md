---
ID: 980
post_title: 'How to PowerPivot outlook data (*.ost or *.pst) data in Microsoft Office Excel 2010'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/01/13/how-to-powerpivot-outlook-data-ost-or-pst-data-in-microsoft-office-excel-2010/
published: true
post_date: 2010-01-13 13:07:44
---
<p>First I extracted some data from the outlook inbox with C# to a CSV file:</p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Text;
<span style="color: blue">using </span>Microsoft.Office.Interop.Outlook;
<span style="color: blue">using </span>System.IO;

<span style="color: blue">namespace </span>Common
{
  <span style="color: blue">public class </span><span style="color: #2b91af">Generator
  </span>{
    <span style="color: blue">const string </span>Splitter = <span style="color: #a31515">&quot;,&quot;</span>;
    <span style="color: blue">const string </span>CsvFIleName = <span style="color: #a31515">&quot;MailData.csv&quot;</span>;
    <span style="color: blue">const string </span>CsvPath = <span style="color: #a31515">@&quot;C:\BDATA&quot;</span>;

    <span style="color: blue">public void </span>Start()
    {
      <span style="color: #2b91af">Application </span>outlook = <span style="color: blue">new </span><span style="color: #2b91af">Application</span>();

      <span style="color: green">// Get the inbox folder
      </span><span style="color: #2b91af">MAPIFolder </span>folder = outlook.GetNamespace(<span style="color: #a31515">&quot;MAPI&quot;</span>).GetDefaultFolder(Microsoft.Office.Interop.Outlook.<span style="color: #2b91af">OlDefaultFolders</span>.olFolderInbox);

      <span style="color: green">// Get received mails
      </span><span style="color: #2b91af">IEnumerable</span>&lt;Microsoft.Office.Interop.Outlook.<span style="color: #2b91af">MailItem</span>&gt; items = folder.Items.OfType&lt;Microsoft.Office.Interop.Outlook.<span style="color: #2b91af">MailItem</span>&gt;();

      <span style="color: green">// Clear file
      </span><span style="color: #2b91af">File</span>.WriteAllText(<span style="color: #2b91af">Path</span>.Combine(CsvPath, CsvFIleName), <span style="color: blue">string</span>.Empty);

      <span style="color: blue">foreach </span>(<span style="color: #2b91af">MailItem </span>item <span style="color: blue">in </span>items)
      {
        <span style="color: #2b91af">StringBuilder </span>csvContent = <span style="color: blue">new </span><span style="color: #2b91af">StringBuilder</span>(<span style="color: blue">string</span>.Empty);

        <span style="color: green">// Add [Sender] to output
        </span><span style="color: blue">if </span>(item.Sender != <span style="color: blue">null </span>&amp;&amp; !<span style="color: blue">string</span>.IsNullOrEmpty(item.Sender.Name)) { csvContent.Append(item.Sender.Name.Replace(Splitter, <span style="color: blue">string</span>.Empty)); }
        csvContent.Append(Splitter);

        <span style="color: green">// Add [Subject] to output
        </span><span style="color: blue">if </span>(!<span style="color: blue">string</span>.IsNullOrEmpty(item.Subject)) { csvContent.Append(item.Subject.Replace(Splitter, <span style="color: blue">string</span>.Empty)); }
        csvContent.Append(Splitter);

        <span style="color: green">// Add [Year] to output
        </span>csvContent.Append(item.ReceivedTime.Year);
        csvContent.Append(Splitter);

        <span style="color: green">// Add [Month] to output
        </span>csvContent.Append(item.ReceivedTime.Month);
        csvContent.Append(Splitter);

        <span style="color: green">// Add [Day] to output
        </span>csvContent.Append(item.ReceivedTime.Day);
        csvContent.Append(Splitter);

        <span style="color: green">// Add [Hour] to output
        </span>csvContent.Append(item.ReceivedTime.Hour);

        <span style="color: green">// Per line export, so you will see the filesize grow on filesystem
        </span><span style="color: blue">using </span>(<span style="color: #2b91af">StreamWriter </span>sw = <span style="color: #2b91af">File</span>.AppendText(<span style="color: #2b91af">Path</span>.Combine(CsvPath, CsvFIleName)))
        {
          sw.WriteLine(csvContent.ToString());
        }
      }
    }
  }
}</pre>
<a href="http://11011.net/software/vspaste"></a>

<ul>
  <li>Open the CSV file with Microsoft Office Excel 2010 and File &gt; Save As “MailData.xlsx”</li>
</ul>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image6.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb6.png" width="606" height="337" /></a> </p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image7.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb7.png" width="610" height="406" /></a> </p>

<ul>
  <li>Click on the ribbon tab [Data], select column A and then click on [Text to Columns]</li>
</ul>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image8.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb8.png" width="617" height="358" /></a> </p>

<ul>
  <li>Click [Delimited] and click [Next]</li>
</ul>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image9.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb9.png" width="599" height="453" /></a> </p>

<ul>
  <li>Uncheck [Tab] and check [Comma], then click [Next]</li>
</ul>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image10.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb10.png" width="608" height="459" /></a> </p>

<ul>
  <li>Click Finish</li>
</ul>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image11.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb11.png" width="517" height="391" /></a> </p>

<ul>
  <li>Result</li>
</ul>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image12.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb12.png" width="587" height="327" /></a> </p>

<ul>
  <li>Press Ctrl + L to create a table</li>
</ul>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image13.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb13.png" width="238" height="148" /></a> </p>

<ul>
  <li>Rename the generated column names (Column1 to Name etc.)</li>
</ul>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image14.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb14.png" width="594" height="326" /></a> </p>

<ul>
  <li>Click on the excel tab [PowerPivot] and click on [Create Linked Table]</li>
</ul>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image15.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb15.png" width="597" height="254" /></a> </p>

<ul>
  <li>In the powerpivot screen add column [Count] with formula [=1]</li>
</ul>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image16.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb16.png" width="589" height="400" /></a> </p>

<ul>
  <li>Click on PivotTable to create a PowerPivot report in Microsoft Excel 2010</li>
</ul>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image17.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb17.png" width="592" height="403" /></a>

  <br /></p>

<ul>
  <li>Click on [Chart and Table (Horizontal)</li>
</ul>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image18.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb18.png" width="408" height="171" /></a> </p>

<ul>
  <li>Click ok</li>

  <li>Select chart</li>

  <li>Drag and drop [Count] to [Values]</li>

  <li>Drag and drop [Name] to [Axis Fields (Categories)]</li>

  <li>Select chart and right click chart</li>

  <li>Click [Change Chart Type]</li>
</ul>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image19.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb19.png" width="600" height="456" /></a> </p>

<ul>
  <li>Select Bar and click [OK]</li>
</ul>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image20.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb20.png" width="601" height="420" /></a> </p>

<ul>
  <li>Click on [Name] in the chart</li>
</ul>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image21.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb21.png" width="598" height="503" /></a> </p>

<ul>
  <li>Choose More Sort Options…</li>
</ul>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image22.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb22.png" width="308" height="349" /></a>

  <br /></p>

<ul>
  <li>Sort [Ascending (A to Z) by] [Sum of Count ]</li>
</ul>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image23.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb23.png" width="604" height="575" /></a> </p>

<p>&#160;</p>

<ul>
  <li>Again click on [Name] in the chart and click [Value Filters] [Greater Than]</li>
</ul>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image24.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb24.png" width="613" height="154" /></a> </p>

<ul>
  <li>The email adresses in the screendumps are partial hidden, but you can see by hovering over the first bar, that [Heide] has send me the most messages [679]</li>
</ul>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image25.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb25.png" width="597" height="568" /></a> </p>

<ul>
  <li>Select chart and Drag and drop [Hour] to [Slicers Horizontal]</li>
</ul>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image26.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb26.png" width="599" height="552" /></a> </p>

<ul>
  <li>If you click on 12 in the hour slicer, you can see [Heide] had sent 49 mails on 12 o’clock</li>
</ul>
---
ID: 1178
post_title: 'How to deploy a report (*.rdl) file to SQL Server Reporting Services using PowerShell'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/30/how-to-deploy-a-report-rdl-file-to-sql-server-reporting-services-using-powershell/
published: true
post_date: 2010-03-30 10:34:56
---
<p>If you want to deploy a report (*.rdl) file to SQL Server Reporting Services in PowerShell, use the following script:</p>  <p>&#160;</p>  <p><strong>PowerShell script</strong></p>  <p>&quot;Set execution policy to [Unrestricted]&quot;    <br />Set-ExecutionPolicy Unrestricted </p>  <p>&quot;Load assembly&quot;   <br />[System.Reflection.Assembly]::LoadFrom(&quot;C:\Temp\Ada.Cdf.dll&quot;) </p>  <p>&quot;Create report&quot;   <br />$report = New-Object Ada.Cdf.Deployment.SSRS.Report    <br />$report.SSRSWebServiceUrl = &quot;<a href="http://localhost/ReportServer/ReportService2005.asmx&quot;">http://localhost/ReportServer/ReportService2005.asmx&quot;</a>    <br />$report.SSRSFolder = &quot;ADA Sales Reports&quot;    <br />$report.FileSystemPath = &quot;C:\Reports\AanvragenStats.rdl&quot;    <br />$report.Create() </p>  <p>&#160;</p>  <p><strong>C# code</strong></p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Text;
<span style="color: blue">using </span>System.IO;
<span style="color: blue">using </span>Ada.Cdf.ReportService2005;

<span style="color: blue">namespace </span>Ada.Cdf.Deployment.SSRS
{
    <span style="color: blue">public class </span><span style="color: #2b91af">Report
    </span>{
        <span style="color: blue">public string </span>FileSystemPath { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
        <span style="color: blue">public string </span>SSRSWebServiceUrl { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
        <span style="color: blue">public string </span>_ssrsFolder = <span style="color: blue">string</span>.Empty;
        <span style="color: blue">public string </span>SSRSFolder 
        {
            <span style="color: blue">get
            </span>{
                <span style="color: green">// Use &quot;/&quot; as default value
                </span><span style="color: blue">string </span>firstCharacter = <span style="color: #a31515">&quot;/&quot;</span>;
                <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(_ssrsFolder))
                {
                    _ssrsFolder = firstCharacter;
                }

                <span style="color: green">// Report folder should start with one &quot;/&quot;
                </span>_ssrsFolder = firstCharacter + _ssrsFolder.TrimStart(firstCharacter.ToCharArray());

                <span style="color: blue">return </span>_ssrsFolder;
            }
            <span style="color: blue">set
            </span>{
                _ssrsFolder = <span style="color: blue">value</span>;
            }
        }

        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Create a report
        </span><span style="color: gray">/// &lt;/summary&gt;
        </span><span style="color: blue">public void </span>Create()
        {

            <span style="color: green">// Validate properties
            </span><span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(<span style="color: blue">this</span>.FileSystemPath)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;this.FileSystemPath&quot;</span>); }
            <span style="color: blue">if </span>(!<span style="color: #2b91af">File</span>.Exists(<span style="color: blue">this</span>.FileSystemPath)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ApplicationException</span>(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;The file [{0}] does not exist&quot;</span>, <span style="color: blue">this</span>.FileSystemPath)); }
            <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(<span style="color: blue">this</span>.SSRSWebServiceUrl)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;this.SSRSWebServiceUrl&quot;</span>); }
            <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(<span style="color: blue">this</span>.SSRSFolder)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;this.SSRSFolder&quot;</span>); }

            <span style="color: green">// Initialize webservice proxy
            </span>ReportService2005.<span style="color: #2b91af">ReportingService2005 </span>rs = <span style="color: blue">new </span>ReportService2005.<span style="color: #2b91af">ReportingService2005</span>();
            rs.Url = <span style="color: blue">this</span>.SSRSWebServiceUrl;
            rs.Credentials = System.Net.<span style="color: #2b91af">CredentialCache</span>.DefaultCredentials;

            <span style="color: green">// Determine filename without extension (used as name in SSRS)
            </span><span style="color: #2b91af">FileInfo </span>fileInfo = <span style="color: blue">new </span><span style="color: #2b91af">FileInfo</span>(<span style="color: blue">this</span>.FileSystemPath);
            <span style="color: blue">string </span>fileNameWithoutExtension = <span style="color: #2b91af">Path</span>.GetFileNameWithoutExtension(fileInfo.FullName);

            <span style="color: green">// Determine filecontents
            </span><span style="color: blue">byte</span>[] fileContents = <span style="color: #2b91af">File</span>.ReadAllBytes(fileInfo.FullName);

            <span style="color: green">// Publish report
            </span><span style="color: #2b91af">Warning</span>[] warnings = rs.CreateReport(fileNameWithoutExtension, <span style="color: blue">this</span>.SSRSFolder, <span style="color: blue">true</span>, fileContents, <span style="color: blue">null</span>);

            <span style="color: green">// Log warnings
            </span><span style="color: blue">if </span>(warnings != <span style="color: blue">null</span>)
            {
                <span style="color: blue">foreach </span>(<span style="color: #2b91af">Warning </span>warning <span style="color: blue">in </span>warnings)
                {
                    <span style="color: #2b91af">Global</span>.Logger.Warn(warning);
                }
            }

        }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Delete a report
        </span><span style="color: gray">/// &lt;/summary&gt;
        </span><span style="color: blue">public void </span>Delete()
        {

            <span style="color: green">// Initialize webservice proxy
            </span>ReportService2005.<span style="color: #2b91af">ReportingService2005 </span>rs = <span style="color: blue">new </span>ReportService2005.<span style="color: #2b91af">ReportingService2005</span>();
            rs.Url = <span style="color: blue">this</span>.SSRSWebServiceUrl;
            rs.Credentials = System.Net.<span style="color: #2b91af">CredentialCache</span>.DefaultCredentials;

            <span style="color: green">// Determine filename without extension (used as name in SSRS)
            </span><span style="color: #2b91af">FileInfo </span>fileInfo = <span style="color: blue">new </span><span style="color: #2b91af">FileInfo</span>(<span style="color: blue">this</span>.FileSystemPath);
            <span style="color: blue">string </span>fileNameWithoutExtension = <span style="color: #2b91af">Path</span>.GetFileNameWithoutExtension(fileInfo.FullName);

            <span style="color: green">// Determine full SSRS path
            </span><span style="color: blue">string </span>ssrsPath = <span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;{0}/{1}&quot;</span>, <span style="color: blue">this</span>.SSRSFolder, fileNameWithoutExtension.TrimStart(<span style="color: #a31515">&quot;/&quot;</span>.ToCharArray()));

            <span style="color: green">// Delete report
            </span>rs.DeleteItem(ssrsPath);

        }
    }
}</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p><strong>Result</strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/03/image32.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/03/image_thumb32.png" width="575" height="304" /></a></p>
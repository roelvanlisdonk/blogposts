---
ID: 1174
post_title: >
  How to deploy a datasource in SQL Server
  Reporting Services with PowerShell
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/30/how-to-deploy-a-datasource-in-sql-server-reporting-services-with-powershell/
published: true
post_date: 2010-03-30 10:26:49
---
<p>If you want to use PowerShell to deploy a datasource in SQL Server Reporting Services use the following script:</p>  <p>&#160;</p>  <p><strong>PowerShell script</strong></p>  <p>&quot;Set execution policy to [Unrestricted]&quot;    <br />Set-ExecutionPolicy Unrestricted </p>  <p>&quot;Load assembly&quot;   <br />[System.Reflection.Assembly]::LoadFrom(&quot;C:\Temp\Ada.Cdf.dll&quot;) </p>  <p>$datasource = New-Object Ada.Cdf.Deployment.SSRS.DataSource   <br />$datasource.SSRSWebServiceUrl = &quot;<a href="http://localhost/ReportServer/ReportService2005.asmx&quot;">http://localhost/ReportServer/ReportService2005.asmx&quot;</a>    <br />$datasource.ImpersonateUser = $false    <br />$datasource.WindowsIntegratedSecurity = $true    <br />$datasource.UserAccountName = &quot;MyDomain\saAsaWeb&quot;    <br />$datasource.UserAccountPassword = &quot;MyPassword&quot;    <br />$datasource.ConnectionString = &quot;Data Source=.;Initial Catalog=AdaSales;Integrated Security=SSPI;&quot;    <br />$datasource.FileSystemPath = &quot;C:\Temp\Reports\AdaSales.rds&quot;    <br />$datasource.SSRSFolder = &quot;ADA Sales Reports&quot;    <br />$datasource.Create()</p>  <p>&#160;</p>  <p>&#160;</p>  <p><strong>C# code</strong></p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Text;
<span style="color: blue">using </span>System.IO;
<span style="color: blue">using </span>Ada.Cdf.ReportService2005;

<span style="color: blue">namespace </span>Ada.Cdf.Deployment.SSRS
{
    <span style="color: blue">public class </span><span style="color: #2b91af">DataSource
    </span>{
        <span style="color: blue">public bool </span>ImpersonateUser { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
        <span style="color: blue">public bool </span>WindowsIntegratedSecurity { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
        <span style="color: blue">public string </span>UserAccountName { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
        <span style="color: blue">public string </span>UserAccountPassword { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
        <span style="color: blue">public string </span>ConnectionString { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
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
        /// </span><span style="color: green">Create a DataSource
        </span><span style="color: gray">/// &lt;/summary&gt;
        </span><span style="color: blue">public void </span>Create()
        {

            <span style="color: green">// Validate properties
            </span><span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(<span style="color: blue">this</span>.FileSystemPath)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;this.FileSystemPath&quot;</span>); }
            <span style="color: blue">if </span>(!<span style="color: #2b91af">File</span>.Exists(<span style="color: blue">this</span>.FileSystemPath)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ApplicationException</span>(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;The file [{0}] does not exist&quot;</span>, <span style="color: blue">this</span>.FileSystemPath)); }
            <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(<span style="color: blue">this</span>.SSRSWebServiceUrl)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;this.SSRSWebServiceUrl&quot;</span>); }
            <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(<span style="color: blue">this</span>.SSRSFolder)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;this.SSRSFolder&quot;</span>); }
            <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(<span style="color: blue">this</span>.UserAccountName)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;this.UserAccountName&quot;</span>); }
            <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(<span style="color: blue">this</span>.UserAccountPassword)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;this.UserAccountPassword&quot;</span>); }

            <span style="color: green">// Initialize webservice proxy
            </span>ReportService2005.<span style="color: #2b91af">ReportingService2005 </span>rs = <span style="color: blue">new </span>ReportService2005.<span style="color: #2b91af">ReportingService2005</span>();
            rs.Url = <span style="color: blue">this</span>.SSRSWebServiceUrl;
            rs.Credentials = System.Net.<span style="color: #2b91af">CredentialCache</span>.DefaultCredentials;

            <span style="color: green">// Determine filename without extension (used as name in SSRS)
            </span><span style="color: #2b91af">FileInfo </span>fileInfo = <span style="color: blue">new </span><span style="color: #2b91af">FileInfo</span>(<span style="color: blue">this</span>.FileSystemPath);
            <span style="color: blue">string </span>fileNameWithoutExtension = <span style="color: #2b91af">Path</span>.GetFileNameWithoutExtension(fileInfo.FullName);    

            <span style="color: green">// Create DataSourceDefinition
            </span><span style="color: #2b91af">DataSourceDefinition </span>definition = <span style="color: blue">new </span><span style="color: #2b91af">DataSourceDefinition</span>();
            definition.CredentialRetrieval = <span style="color: #2b91af">CredentialRetrievalEnum</span>.Store;
            definition.ConnectString = <span style="color: blue">this</span>.ConnectionString;
            definition.UserName = <span style="color: blue">this</span>.UserAccountName;
            definition.Password = <span style="color: blue">this</span>.UserAccountPassword;
            definition.Enabled = <span style="color: blue">true</span>;
            definition.EnabledSpecified = <span style="color: blue">true</span>;
            definition.Extension = <span style="color: #a31515">&quot;SQL&quot;</span>;
            definition.ImpersonateUser = <span style="color: blue">this</span>.ImpersonateUser;
            definition.ImpersonateUserSpecified = <span style="color: blue">true</span>;

            <span style="color: green">// Use the default prompt string
            </span>definition.Prompt = <span style="color: blue">null</span>;
            definition.WindowsCredentials = <span style="color: blue">this</span>.WindowsIntegratedSecurity;

            <span style="color: green">// Create datasource
            </span>rs.CreateDataSource(fileNameWithoutExtension, <span style="color: blue">this</span>.SSRSFolder, <span style="color: blue">true</span>, definition, <span style="color: blue">null</span>);

        }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Delete a DataSource
        </span><span style="color: gray">/// &lt;/summary&gt;
        </span><span style="color: blue">public void </span>Delete()
        {
            <span style="color: green">// Validate properties
            </span><span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(<span style="color: blue">this</span>.FileSystemPath)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;this.FileSystemPath&quot;</span>); }
            <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(<span style="color: blue">this</span>.SSRSWebServiceUrl)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;this.SSRSWebServiceUrl&quot;</span>); }
            <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(<span style="color: blue">this</span>.SSRSFolder)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;this.SSRSFolder&quot;</span>); }

            <span style="color: green">// Initialize webservice proxy
            </span>ReportService2005.<span style="color: #2b91af">ReportingService2005 </span>rs = <span style="color: blue">new </span>ReportService2005.<span style="color: #2b91af">ReportingService2005</span>();
            rs.Url = <span style="color: blue">this</span>.SSRSWebServiceUrl;
            rs.Credentials = System.Net.<span style="color: #2b91af">CredentialCache</span>.DefaultCredentials;

            <span style="color: green">// Determine filename without extension (used as name in SSRS)
            </span><span style="color: #2b91af">FileInfo </span>fileInfo = <span style="color: blue">new </span><span style="color: #2b91af">FileInfo</span>(<span style="color: blue">this</span>.FileSystemPath);
            <span style="color: blue">string </span>fileNameWithoutExtension = <span style="color: #2b91af">Path</span>.GetFileNameWithoutExtension(fileInfo.FullName);

            <span style="color: green">// Determine full SSRS path
            </span><span style="color: blue">string </span>ssrsPath = <span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;{0}/{1}&quot;</span>, <span style="color: blue">this</span>.SSRSFolder, fileNameWithoutExtension.TrimStart(<span style="color: #a31515">&quot;/&quot;</span>.ToCharArray()));

            <span style="color: green">// Delete datasource
            </span>rs.DeleteItem(ssrsPath);

        }
    }
}</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p>&#160;</p>

<p><strong>Result</strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/03/image31.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/03/image_thumb31.png" width="634" height="704" /></a></p>
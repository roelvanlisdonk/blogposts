---
ID: 1171
post_title: >
  How to create a folder in SQL Server
  Reporting Services with PowerShell
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/30/how-to-create-a-folder-in-sql-server-reporting-services-with-powershell/
published: true
post_date: 2010-03-30 10:19:19
---
<p>If you want to use PowerShell to create a folder in SQL Server Reporting Services use the following script:   <br />    <br />    <br /><strong>PowerShell script</strong>    <br /></p>  <p>&quot;Set execution policy to [Unrestricted]&quot;    <br />Set-ExecutionPolicy Unrestricted </p>  <p>&quot;Load assembly&quot;   <br />[System.Reflection.Assembly]::LoadFrom(&quot;C:\Temp\Ada.Cdf.dll&quot;) </p>  <p>$folder = New-Object Ada.Cdf.Deployment.SSRS.Folder   <br />$folder.SSRSWebServiceUrl = &quot;<a href="http://localhost/ReportServer/ReportService2005.asmx&quot;">http://localhost/ReportServer/ReportService2005.asmx&quot;</a>    <br />$folder.Name = &quot;ADA Sales Reports&quot;    <br />$folder.Parent = &quot;/&quot;    <br />$folder.Create()</p>  <p>&#160;</p>  <p>&#160;</p>  <p>&#160;</p>  <p><strong>C# Code</strong></p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Text;
<span style="color: blue">using </span>System.IO;

<span style="color: blue">namespace </span>Ada.Cdf.Deployment.SSRS
{
    <span style="color: blue">public class </span><span style="color: #2b91af">Folder
    </span>{
        <span style="color: blue">public string </span>SSRSWebServiceUrl { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }
        <span style="color: blue">public string </span>_parent = <span style="color: #a31515">&quot;/&quot;</span>;
        <span style="color: blue">public string </span>Parent
        {
            <span style="color: blue">get
            </span>{
                <span style="color: green">// Use &quot;/&quot; as default value
                </span><span style="color: blue">string </span>firstCharacter = <span style="color: #a31515">&quot;/&quot;</span>;
                <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(_parent))
                {
                    _parent = firstCharacter;
                }

                <span style="color: green">// Parent should start with one &quot;/&quot;
                </span>_parent = firstCharacter + _parent.TrimStart(firstCharacter.ToCharArray());

                <span style="color: blue">return </span>_parent;
            }
            <span style="color: blue">set
            </span>{
                _parent = <span style="color: blue">value</span>;
            }
        }
        <span style="color: blue">public string </span>_name = <span style="color: blue">string</span>.Empty;
        <span style="color: blue">public string </span>Name
        {
            <span style="color: blue">get
            </span>{
                
                <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(_name))
                {
                    _name = <span style="color: blue">string</span>.Empty;
                }

                <span style="color: green">// FolderName should not start with&quot;/&quot;
                </span>_name = _name.TrimStart(<span style="color: #a31515">&quot;/&quot;</span>.ToCharArray());

                <span style="color: blue">return </span>_name;
            }
            <span style="color: blue">set
            </span>{
                _name = <span style="color: blue">value</span>;
            }
        }

        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Create a report
        </span><span style="color: gray">/// &lt;/summary&gt;
        </span><span style="color: blue">public void </span>Create()
        {

            <span style="color: green">// Validate properties
            </span><span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(<span style="color: blue">this</span>.SSRSWebServiceUrl)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;this.SSRSWebServiceUrl&quot;</span>); }
            <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(<span style="color: blue">this</span>.Name)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;this.Name&quot;</span>); }
            <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(<span style="color: blue">this</span>.Parent)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;this.Parent&quot;</span>); }

            <span style="color: green">// Initialize webservice proxy
            </span>ReportService2005.<span style="color: #2b91af">ReportingService2005 </span>rs = <span style="color: blue">new </span>ReportService2005.<span style="color: #2b91af">ReportingService2005</span>();
            rs.Url = <span style="color: blue">this</span>.SSRSWebServiceUrl;
            rs.Credentials = System.Net.<span style="color: #2b91af">CredentialCache</span>.DefaultCredentials;

            <span style="color: blue">try
            </span>{
                rs.
                <span style="color: green">// Create report folder, this will throw an exception if the folder already exists
                </span>rs.CreateFolder(<span style="color: blue">this</span>.Name, <span style="color: blue">this</span>.Parent, <span style="color: blue">null</span>);
            }
            <span style="color: blue">catch </span>(<span style="color: #2b91af">Exception </span>ex)
            {
                <span style="color: #2b91af">Global</span>.Logger.Info(<span style="color: #a31515">&quot;Folder already exists&quot;</span>, ex);
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

            <span style="color: green">// Determine full SSRS path
            </span><span style="color: blue">string </span>ssrsPath = <span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;{0}/{1}&quot;</span>, <span style="color: blue">this</span>.Parent.TrimStart(<span style="color: #a31515">&quot;/&quot;</span>.ToCharArray()), <span style="color: blue">this</span>.Name);

            <span style="color: green">// Delete report
            </span>rs.DeleteItem(ssrsPath);

       }
    }
}</pre>
<a href="http://11011.net/software/vspaste"></a>

<p><strong>Result</strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/03/image30.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/03/image_thumb30.png" width="1000" height="784" /></a></p>
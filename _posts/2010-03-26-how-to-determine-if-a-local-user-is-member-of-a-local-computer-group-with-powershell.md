---
ID: 1158
post_title: 'How to determine if a local user is member of a local computer group before adding, with PowerShell and C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/26/how-to-determine-if-a-local-user-is-member-of-a-local-computer-group-with-powershell/
published: true
post_date: 2010-03-26 16:11:43
---
<p>To dermine if a local user is member of a local group, before adding the user to the local group in PowerShell I use a C# class. The C# class could be converted to pure PowerShell code, but I prefer the C# class with it’s using statements:   <br />    <br /></p>  <p>&#160;</p>  <p><font size="4"><strong>[PowerShell script]</strong></font>    <br /></p>  <p>&quot;Set execution policy to [Unrestricted]&quot;    <br />Set-ExecutionPolicy Unrestricted</p>  <p>$ComputerName = &quot;.&quot;   <br />$ServiceAccountWebUserName = &quot;\saWeb&quot;,</p>  <p>&quot;Check if user is member of IIS_IUSRS&quot;   <br />$localGroup = New-Object Ada.Cdf.Deployment.LocalGroup    <br />$localGroup.ComputerName = $ComputerName    <br />$localGroup.Name = &quot;IIS_IUSRS&quot;    <br />if(!$localGroup.ContainsUser($ServiceAccountWebUserName))    <br />{    <br />&#160;&#160;&#160; &quot;Add user to the IIS_IUSRS group&quot;    <br />&#160;&#160;&#160; $localGroup.AddUser($ServiceAccountWebUserName)    <br />}</p>  <p>   <br />    <br />    <br /><strong><font size="4">[C# Class]</font></strong></p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Text;
<span style="color: blue">using </span>System.DirectoryServices;
<span style="color: blue">using </span>System.Collections;

<span style="color: blue">namespace </span>Ada.Cdf.Deployment
{
    <span style="color: blue">public class </span><span style="color: #2b91af">LocalGroup
    </span>{
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Name of the computer use &quot;.&quot; for executing computer
        </span><span style="color: gray">/// &lt;/summary&gt;
        </span><span style="color: blue">string </span>_computerName = <span style="color: #2b91af">Environment</span>.MachineName;
        <span style="color: blue">public string </span>ComputerName 
        {
            <span style="color: blue">get
            </span>{
                <span style="color: blue">if </span>(!<span style="color: blue">string</span>.IsNullOrEmpty(_computerName) &amp;&amp; _computerName.Equals(<span style="color: #a31515">&quot;.&quot;</span>))
                {
                    _computerName = <span style="color: #2b91af">Environment</span>.MachineName;
                }
                <span style="color: blue">return </span>_computerName;
            }
            <span style="color: blue">set
            </span>{
                _computerName = <span style="color: blue">value</span>;
            }
        }
        <span style="color: blue">public string </span>Name { <span style="color: blue">get</span>; <span style="color: blue">set</span>; }

        <span style="color: gray">/// &lt;summary&gt;
        /// 
        /// &lt;/summary&gt;
        /// &lt;param name=&quot;userName&quot;&gt;&lt;/param&gt;
        /// &lt;returns&gt;&lt;/returns&gt;
        </span><span style="color: blue">public bool </span>ContainsUser(<span style="color: blue">string </span>userName)
        {

            <span style="color: green">// Validate properties
            </span><span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(<span style="color: blue">this</span>.ComputerName)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;this.ComputerName&quot;</span>); }
            <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(<span style="color: blue">this</span>.Name)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;this.Name&quot;</span>); }

            <span style="color: blue">bool </span>result = <span style="color: blue">false</span>;
            <span style="color: blue">using </span>(<span style="color: #2b91af">DirectoryEntry </span>groupEntry = <span style="color: blue">new </span><span style="color: #2b91af">DirectoryEntry</span>(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;WinNT://{0}/{1},group&quot;</span>, <span style="color: blue">this</span>.ComputerName, <span style="color: blue">this</span>.Name)))
            {
                <span style="color: green">// Get group members
                </span><span style="color: #2b91af">IEnumerable </span>groupMembers = (<span style="color: #2b91af">IEnumerable</span>)groupEntry.Invoke(<span style="color: #a31515">&quot;Members&quot;</span>);

                <span style="color: green">// Loop members
                </span><span style="color: blue">foreach </span>(<span style="color: blue">object </span>member <span style="color: blue">in </span>groupMembers)
                {
                    <span style="color: blue">using </span>(<span style="color: #2b91af">DirectoryEntry </span>memberEntry = <span style="color: blue">new </span><span style="color: #2b91af">DirectoryEntry</span>(member))
                    {
                        <span style="color: blue">if </span>(memberEntry.Name.ToLower().Equals(userName.ToLower()))
                        {
                            result = <span style="color: blue">true</span>;
                        }
                    }
                }
            }

            <span style="color: blue">return </span>result;
        }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Add a local user to a local group
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;userName&quot;&gt;&lt;/param&gt;
        </span><span style="color: blue">public void </span>AddUser(<span style="color: blue">string </span>userName)
        {

            <span style="color: green">// Validate properties
            </span><span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(<span style="color: blue">this</span>.ComputerName)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;this.ComputerName&quot;</span>); }
            <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(<span style="color: blue">this</span>.Name)) { <span style="color: blue">throw new </span><span style="color: #2b91af">ArgumentNullException</span>(<span style="color: #a31515">&quot;this.Name&quot;</span>); }

            <span style="color: blue">using </span>(<span style="color: #2b91af">DirectoryEntry </span>groupEntry = <span style="color: blue">new </span><span style="color: #2b91af">DirectoryEntry</span>(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;WinNT://{0}/{1},group&quot;</span>, <span style="color: blue">this</span>.ComputerName, <span style="color: blue">this</span>.Name)))
            {
              <span style="color: green">// Add user to group
              </span>groupEntry.Invoke(<span style="color: #a31515">&quot;Add&quot;</span>, <span style="color: blue">new object</span>[] { <span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;WinNT://{0}/{1}&quot;</span>, <span style="color: blue">this</span>.ComputerName, userName) });
            }

        }
    }
}</pre>
<a href="http://11011.net/software/vspaste"></a>
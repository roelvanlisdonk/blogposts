---
ID: 715
post_title: >
  Create custom eventlog during setup, by
  reading log4net configuration file.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/09/23/create-custom-eventlog-during-setup-by-reading-log4net-configuration-file/
published: true
post_date: 2009-09-23 11:24:45
---
<p>If you want to create a customeventlog during setup, in a custom action. You can open a App.config file containing the log4net configuration and read the settings from that file at runtime.   <br />You also can add appenders or remove appenders at runtime, but in this case I just wanted to read the configuration and create a custom eventlog:    <br />    <br /></p>  <pre class="code"><span style="color: blue">       private string </span>_productInstallationFolder = <span style="color: blue">null</span>;
       <span style="color: gray">/// &lt;summary&gt;
       /// </span><span style="color: green">Returns C:\Program Files\MyCompany\MyProduct or C:\Program Files (x86)\MyCompany\MyProduct depending on the platform.
       </span><span style="color: gray">/// &lt;/summary&gt;
       </span><span style="color: blue">public string </span>ProductInstallationFolder
       {
           <span style="color: blue">get
           </span>{
               <span style="color: blue">if </span>(<span style="color: blue">string</span>.IsNullOrEmpty(_productInstallationFolder))
               {
                   <span style="color: blue">var </span>programFilesFolder = System.<span style="color: #2b91af">Environment</span>.GetFolderPath(System.<span style="color: #2b91af">Environment</span>.<span style="color: #2b91af">SpecialFolder</span>.ProgramFiles);
                   _productInstallationFolder = <span style="color: #2b91af">Path</span>.Combine(programFilesFolder, <span style="color: #a31515">@&quot;MyCompany\MyProduct&quot;</span>);
               }
               <span style="color: blue">return </span>_productInstallationFolder;
           }
           <span style="color: blue">set
           </span>{
               _productInstallationFolder = <span style="color: blue">value</span>;
           }
       }
       <span style="color: blue">public void </span>CreateCustomEventLog()
       {
           <span style="color: #2b91af">XmlConfigurator</span>.Configure(<span style="color: blue">new </span><span style="color: #2b91af">FileInfo</span>(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;{0}.config&quot;</span>, <span style="color: blue">this</span>.ProductInstallationFolder))); <br />           <span style="color: blue">var </span>repository = LogManager.GetRepository() <span style="color: blue">as </span>Hierarchy;
           <span style="color: blue">if </span>(repository != <span style="color: blue">null</span>)
           {
               <span style="color: blue">var </span>appenders = repository.GetAppenders();
               <span style="color: blue">if </span>(appenders != <span style="color: blue">null</span>)
               {
                   <span style="color: blue">foreach </span>(<span style="color: blue">var </span>appender <span style="color: blue">in </span>appenders)
                   {
                       <span style="color: blue">if </span>(appender <span style="color: blue">is </span>EventLogAppender)
                       {
                           <span style="color: blue">var </span>eventLogAppender = appender <span style="color: blue">as </span>EventLogAppender;
                           <span style="color: #2b91af">EventLog</span>.CreateEventSource(eventLogAppender.ApplicationName, eventLogAppender.LogName);
                           <span style="color: green">// Close application to allow the Windows eventlog service to refresh.
                           // When applcation is restarted the first log event will create the log file.
                       </span>}
                   }
               }
           }
       }</pre>
<a href="http://11011.net/software/vspaste"></a>
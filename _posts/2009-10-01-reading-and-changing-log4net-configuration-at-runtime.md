---
ID: 723
post_title: >
  Reading and changing Log4Net
  configuration at runtime
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/10/01/reading-and-changing-log4net-configuration-at-runtime/
published: true
post_date: 2009-10-01 10:59:17
---
<p>You can read and change the Log4Net configuration at runtime, the following code, shows the eventlogname en eventlogsource for each eventlogappender defined, but if you change the eventLogAppender object properties the configuration will be changed.    <br /></p>  <pre class="code"><span style="color: #2b91af">            XmlConfigurator</span>.Configure(<span style="color: blue">new </span><span style="color: #2b91af">FileInfo</span>(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;{0}.config&quot;</span>, <span style="color: #a31515">@&quot;C:\Temp\TestApplication.exe.config&quot;</span>)));
            <span style="color: blue">var </span>repository = <span style="color: #2b91af">LogManager</span>.GetRepository() <span style="color: blue">as </span><span style="color: #2b91af">Hierarchy</span>;
            <span style="color: blue">if </span>(repository != <span style="color: blue">null</span>)
            {
                <span style="color: blue">var </span>appenders = repository.GetAppenders();
                <span style="color: blue">if </span>(appenders != <span style="color: blue">null</span>)
                {
                    <span style="color: blue">foreach </span>(<span style="color: blue">var </span>appender <span style="color: blue">in </span>appenders)
                    {
                        <span style="color: blue">if </span>(appender <span style="color: blue">is </span><span style="color: #2b91af">EventLogAppender</span>)
                        {
                            <span style="color: blue">var </span>eventLogAppender = appender <span style="color: blue">as </span><span style="color: #2b91af">EventLogAppender</span>;
                            <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;Eventlogname [{0}] and Eventlogsource [{1}] &quot;</span>, eventLogAppender.LogName, eventLogAppender.ApplicationName));
                        }
                    }
                }
            }</pre>
<a href="http://11011.net/software/vspaste"></a>
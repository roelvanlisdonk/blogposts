---
ID: 1130
post_title: 'Log4Net error when using a renderer in you&rsquo;re App.config or Web.config'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/16/log4net-error-when-using-a-renderer-in-youre-app-config-or-web-config/
published: true
post_date: 2010-03-16 12:02:22
---
<p>If you use a Log4Net renderer in you’re App.config, you might get the error:</p>  <p>Error: log4net:ERROR XmlHierarchyConfigurator: Cannot find Property [renderer] to set object on [log4net.Repository.Hierarchy.RootLogger]   <br />log4net:ERROR XmlHierarchyConfigurator: Cannot find Property [renderer] to set object on [log4net.Repository.Hierarchy.RootLogger]</p>  <p>&#160;</p>  <p><strong>Solution</strong></p>  <p>Place the &lt;renderer&gt; tag not in the &lt;root&gt; tag, but in the &lt;log4net&gt; tag.</p>  <p>&#160;</p>  <p><strong>App.config</strong></p>  <pre class="code"><span style="color: blue">&lt;?</span><span style="color: #a31515">xml </span><span style="color: red">version</span><span style="color: blue">=</span>&quot;<span style="color: blue">1.0</span>&quot; <span style="color: red">encoding</span><span style="color: blue">=</span>&quot;<span style="color: blue">utf-8</span>&quot; <span style="color: blue">?&gt;
&lt;</span><span style="color: #a31515">configuration</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">configSections</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">section </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net.Config.Log4NetConfigurationSectionHandler,log4net, Version=1.2.10.0, Culture=neutral, PublicKeyToken=1b44e1d426115821</span>&quot; <span style="color: blue">/&gt;
    &lt;/</span><span style="color: #a31515">configSections</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">log4net</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">appender </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">ConsoleAppender</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net.Appender.ConsoleAppender</span>&quot;<span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">layout </span><span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net.Layout.PatternLayout</span>&quot;<span style="color: blue">&gt;
                &lt;</span><span style="color: #a31515">conversionPattern </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">%type.%method() %message%newline</span>&quot; <span style="color: blue">/&gt;
            &lt;/</span><span style="color: #a31515">layout</span><span style="color: blue">&gt;
        &lt;/</span><span style="color: #a31515">appender</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">appender </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">EventLogAppender</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net.Appender.EventLogAppender</span>&quot;<span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">param </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">LogName</span>&quot; <span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">Application</span>&quot; <span style="color: blue">/&gt;
            &lt;</span><span style="color: #a31515">applicationName </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">Ada.Cdf.Test</span>&quot; <span style="color: blue">/&gt;
            &lt;</span><span style="color: #a31515">layout </span><span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net.Layout.PatternLayout</span>&quot;<span style="color: blue">&gt;
                &lt;</span><span style="color: #a31515">conversionPattern </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">%type.%method()%newline%newline%message%newline</span>&quot; <span style="color: blue">/&gt;
            &lt;/</span><span style="color: #a31515">layout</span><span style="color: blue">&gt;
        &lt;/</span><span style="color: #a31515">appender</span><span style="color: blue">&gt;
        <font size="4">&lt;</font></span><font size="4"><span style="color: #a31515">renderer </span><span style="color: red">renderingClass</span><span style="color: blue">=</span>&quot;<span style="color: blue">Ada.Cdf.Logging.ExceptionRenderer, Ada.Cdf</span>&quot; <span style="color: red">renderedClass</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Exception</span>&quot; </font><span style="color: blue"><font size="4">/&gt;</font>
        &lt;</span><span style="color: #a31515">root</span><span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">level </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">ALL</span>&quot; <span style="color: blue">/&gt;
            &lt;</span><span style="color: #a31515">appender-ref </span><span style="color: red">ref</span><span style="color: blue">=</span>&quot;<span style="color: blue">EventLogAppender</span>&quot; <span style="color: blue">/&gt;
            &lt;</span><span style="color: #a31515">appender-ref </span><span style="color: red">ref</span><span style="color: blue">=</span>&quot;<span style="color: blue">ConsoleAppender</span>&quot; <span style="color: blue">/&gt;
        &lt;/</span><span style="color: #a31515">root</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">log4net</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">configuration</span><span style="color: blue">&gt;</span></pre>
<a href="http://11011.net/software/vspaste"></a>
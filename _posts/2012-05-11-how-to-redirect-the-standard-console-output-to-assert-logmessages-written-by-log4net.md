---
ID: 2674
post_title: >
  How to redirect the standard console
  output, to assert logmessages written by
  log4net.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/05/11/how-to-redirect-the-standard-console-output-to-assert-logmessages-written-by-log4net/
published: true
post_date: 2012-05-11 14:54:00
---
<p>By using a log4net ConsoleAppender, you can write all log messages in your application to the console. These message will show up in the Microsoft Visual Studio output window. I needed a way to redirect the messages written to the console, so I could verify if the correct messages were send to the console. For this task I redirected the standard console output in my unit test:</p>  <p>&#160;</p>  <p><strong><font size="3">Code</font></strong></p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.IO;
<span style="color: blue">using </span>System.Text;
<span style="color: blue">using </span>log4net;
<span style="color: blue">using </span>log4net.Config;
<span style="color: blue">using </span>Microsoft.VisualStudio.TestTools.UnitTesting;

<span style="color: blue">namespace </span>TestProject1
{
    [<span style="color: #2b91af">TestClass</span>]
    <span style="color: blue">public class </span><span style="color: #2b91af">UnitTest1
    </span>{
        [<span style="color: #2b91af">TestMethod</span>]
        <span style="color: blue">public void </span>TestMethod1()
        {
            <span style="color: green">// Save original console output writer.
            </span><span style="color: #2b91af">TextWriter </span>originalConsole = <span style="color: #2b91af">Console</span>.Out;

            <span style="color: green">// Configure log4net based on the App.config
            </span><span style="color: #2b91af">XmlConfigurator</span>.Configure();

            <span style="color: blue">var </span>builder = <span style="color: blue">new </span><span style="color: #2b91af">StringBuilder</span>();
            <span style="color: blue">using </span>(<span style="color: blue">var </span>writer = <span style="color: blue">new </span><span style="color: #2b91af">StringWriter</span>(builder))
            {
                <span style="color: green">// Redirect all Console messages to the StringWriter.
                </span><span style="color: #2b91af">Console</span>.SetOut(writer);

                <span style="color: green">// Log a debug message.
                </span><span style="color: #2b91af">ILog </span>logger = <span style="color: #2b91af">LogManager</span>.GetLogger(<span style="color: #a31515">&quot;Unittest logger&quot;</span>);
                logger.Debug(<span style="color: #a31515">&quot;This is a debug message&quot;</span>);
            }

            <span style="color: green">// Get all messages written to the console.
            </span><span style="color: blue">string </span>consoleOutput = <span style="color: blue">string</span>.Empty;
            <span style="color: blue">using </span>(<span style="color: blue">var </span>reader = <span style="color: blue">new </span><span style="color: #2b91af">StringReader</span>(builder.ToString()))
            {
                consoleOutput = reader.ReadToEnd();
            }

            <span style="color: green">// Assert.
            </span><span style="color: blue">string </span>expected = <span style="color: #a31515">&quot;This is a debug message&quot; </span>+ <span style="color: #2b91af">Environment</span>.NewLine;
            <span style="color: #2b91af">Assert</span>.AreEqual(expected, consoleOutput);

            <span style="color: green">// Redirect back to original console output.
            </span><span style="color: #2b91af">Console</span>.SetOut(originalConsole);
        }
    }
}</pre>


<p><strong><font size="3">App.config</font></strong></p>

<p>&#160;</p>

<pre class="code"><span style="color: blue">&lt;?</span><span style="color: #a31515">xml </span><span style="color: red">version</span><span style="color: blue">=</span>&quot;<span style="color: blue">1.0</span>&quot;<span style="color: blue">?&gt;
&lt;</span><span style="color: #a31515">configuration</span><span style="color: blue">&gt;
  &lt;</span><span style="color: #a31515">configSections</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">section </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net.Config.Log4NetConfigurationSectionHandler,log4net</span>&quot;<span style="color: blue">/&gt;
  &lt;/</span><span style="color: #a31515">configSections</span><span style="color: blue">&gt;
  &lt;</span><span style="color: #a31515">log4net</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">appender </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">ConsoleAppender</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net.Appender.ConsoleAppender</span>&quot;<span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">layout </span><span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net.Layout.PatternLayout</span>&quot;<span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">conversionPattern </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">%message%newline</span>&quot; <span style="color: blue">/&gt;
      &lt;/</span><span style="color: #a31515">layout</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">appender</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">root</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">level </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">DEBUG</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">appender-ref </span><span style="color: red">ref</span><span style="color: blue">=</span>&quot;<span style="color: blue">ConsoleAppender</span>&quot; <span style="color: blue">/&gt;
    &lt;/</span><span style="color: #a31515">root</span><span style="color: blue">&gt;
  &lt;/</span><span style="color: #a31515">log4net</span><span style="color: blue">&gt;
  &lt;</span><span style="color: #a31515">startup</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">supportedRuntime </span><span style="color: red">version</span><span style="color: blue">=</span>&quot;<span style="color: blue">v4.0</span>&quot; <span style="color: red">sku</span><span style="color: blue">=</span>&quot;<span style="color: blue">.NETFramework,Version=v4.0</span>&quot;<span style="color: blue">/&gt;
  &lt;/</span><span style="color: #a31515">startup</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">configuration</span><span style="color: blue">&gt;

</span></pre>


<p><strong><font size="3">Microsoft Visual Studio</font></strong></p>

<p>&#160;</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/05/image6.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/05/image_thumb6.png" width="461" height="352" /></a></p>

<p>&#160;</p>

<p>I used NuGet to add a reference to the latest log4net build.</p>
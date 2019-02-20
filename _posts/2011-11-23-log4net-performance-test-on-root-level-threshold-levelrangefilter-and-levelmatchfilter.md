---
ID: 2258
post_title: 'Log4net performance test on [Root &gt; Level], [Threshold], [LevelRangeFilter] and [LevelMatchFilter]'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/11/23/log4net-performance-test-on-root-level-threshold-levelrangefilter-and-levelmatchfilter/
published: true
post_date: 2011-11-23 09:43:30
---
<p>In many cases you want to allow only ERROR logging in production for performance reasons.</p>  <p>I did a little experiment on log4net performance, based on different configurations in the App.config, to try and find out what the best settings are for only allowing ERROR logging in production.</p>  <p>&#160;</p>  <p><strong><font size="3">First some explanation on the log4net settings used</font></strong></p>  <p>1. The [Root &gt; Level] is used to only allow logging based on the given value and above for all appenders. </p>  <p>2. The threshold setting is used to allow logging for the given value and above for a specific appender.</p>  <p>3. LevelMatchFiler is used to allow only logging for a specified level for a specific appender.</p>  <p>4. LevelRangeFilter is used to allow only logging between the given values for a specific appender.</p>  <p>&#160;</p>  <h2><font size="3"><font style="font-weight: bold">The App.config with all settings</font></font></h2>  <p><font color="#c0504d">This App.config shows all settings used, it is not a working App.config.</font></p>  <pre class="code"><span style="color: blue">&lt;?</span><span style="color: #a31515">xml </span><span style="color: red">version</span><span style="color: blue">=</span>&quot;<span style="color: blue">1.0</span>&quot; <span style="color: red">encoding</span><span style="color: blue">=</span>&quot;<span style="color: blue">utf-8</span>&quot; <span style="color: blue">?&gt;
&lt;</span><span style="color: #a31515">configuration</span><span style="color: blue">&gt;
  &lt;</span><span style="color: #a31515">configSections</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">section </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net.Config.Log4NetConfigurationSectionHandler, log4net</span>&quot; <span style="color: blue">/&gt;
  &lt;/</span><span style="color: #a31515">configSections</span><span style="color: blue">&gt;
  &lt;</span><span style="color: #a31515">log4net</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">appender </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">RollingLogFileAppender</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net.Appender.RollingFileAppender</span>&quot;<span style="color: blue">&gt;
      &lt;!-- </span><span style="color: green">Allow only ERROR logging for this adapter </span><span style="color: blue">--&gt;
      &lt;</span><span style="color: #a31515">threshold </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">ERROR</span>&quot;<span style="color: blue">/&gt;

      &lt;!-- </span><span style="color: green">Allow only ERROR logging for this adapter </span><span style="color: blue">--&gt;
      &lt;</span><span style="color: #a31515">filter </span><span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net.Filter.LevelMatchFilter</span>&quot;<span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">acceptOnMatch </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">true</span>&quot; <span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">levelToMatch  </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">ERROR</span>&quot; <span style="color: blue">/&gt;
      &lt;/</span><span style="color: #a31515">filter</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">filter </span><span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net.Filter.DenyAllFilter</span>&quot; <span style="color: blue">/&gt;

      &lt;!-- </span><span style="color: green">Allow only DEBUG, INFO, WARN and ERROR logging for this adapter </span><span style="color: blue">--&gt;
      &lt;</span><span style="color: #a31515">filter </span><span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net.Filter.LevelRangeFilter</span>&quot;<span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">acceptOnMatch </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">true</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">levelMin </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">DEBUG</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">levelMax </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">ERROR</span>&quot;<span style="color: blue">/&gt;
      &lt;/</span><span style="color: #a31515">filter</span><span style="color: blue">&gt;
      
      &lt;</span><span style="color: #a31515">file </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">Log.txt</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">appendToFile </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">true</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">rollingStyle </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">Size</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">maxSizeRollBackups </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">1</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">maximumFileSize </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">100MB</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">staticLogFileName </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">true</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">layout </span><span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net.Layout.PatternLayout</span>&quot;<span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">conversionPattern </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">%date %-5level %type.%method - %message%newline</span>&quot;<span style="color: blue">/&gt;
      &lt;/</span><span style="color: #a31515">layout</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">appender</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">appender </span><span style="color: red">name</span><span style="color: blue">=</span>&quot;<span style="color: blue">ADONetAppender</span>&quot; <span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net.Appender.ADONetAppender</span>&quot;<span style="color: blue">&gt;
      &lt;!-- </span><span style="color: green">Allow only ERROR logging for this adapter </span><span style="color: blue">--&gt;
      &lt;</span><span style="color: #a31515">threshold </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">ERROR</span>&quot;<span style="color: blue">/&gt;
      
      &lt;!-- </span><span style="color: green">Allow only ERROR logging for this adapter </span><span style="color: blue">--&gt;
      &lt;</span><span style="color: #a31515">filter </span><span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net.Filter.LevelMatchFilter</span>&quot;<span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">acceptOnMatch </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">true</span>&quot; <span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">levelToMatch  </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">ERROR</span>&quot; <span style="color: blue">/&gt;
      &lt;/</span><span style="color: #a31515">filter</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">filter </span><span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net.Filter.DenyAllFilter</span>&quot; <span style="color: blue">/&gt;
      
      &lt;!-- </span><span style="color: green">Allow only DEBUG, INFO, WARN and ERROR logging for this adapter </span><span style="color: blue">--&gt;
      &lt;</span><span style="color: #a31515">filter </span><span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net.Filter.LevelRangeFilter</span>&quot;<span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">acceptOnMatch </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">true</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">levelMin </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">DEBUG</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">levelMax </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">ERROR</span>&quot;<span style="color: blue">/&gt;
      &lt;/</span><span style="color: #a31515">filter</span><span style="color: blue">&gt;
      
      &lt;</span><span style="color: #a31515">bufferSize </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">1</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">connectionType </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">System.Data.SqlClient.SqlConnection, System.Data, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">commandText </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">INSERT INTO Log ([Date],[Thread],[Level],[Logger],[Message]) VALUES (@log_date, @thread, @log_level, @logger, @message)</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">connectionString </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">Data Source=myserver.dev.nl\dev2008;Initial Catalog=MyDatabase;Integrated Security=SSPI</span>&quot;<span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">parameter</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">parameterName </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">@log_date</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">dbType </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">DateTime</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">layout </span><span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net.Layout.PatternLayout</span>&quot; <span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">%date{yyyy'-'MM'-'dd HH':'mm':'ss'.'fff}</span>&quot;<span style="color: blue">/&gt;
      &lt;/</span><span style="color: #a31515">parameter</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">parameter</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">parameterName </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">@thread</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">dbType </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">String</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">size </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">255</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">layout </span><span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net.Layout.PatternLayout</span>&quot; <span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">%thread</span>&quot;<span style="color: blue">/&gt;
      &lt;/</span><span style="color: #a31515">parameter</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">parameter</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">parameterName </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">@log_level</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">dbType </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">String</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">size </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">50</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">layout </span><span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net.Layout.PatternLayout</span>&quot; <span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">%level</span>&quot;<span style="color: blue">/&gt;
      &lt;/</span><span style="color: #a31515">parameter</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">parameter</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">parameterName </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">@logger</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">dbType </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">String</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">size </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">255</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">layout </span><span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net.Layout.PatternLayout</span>&quot; <span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">%type.%method</span>&quot;<span style="color: blue">/&gt;
      &lt;/</span><span style="color: #a31515">parameter</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">parameter</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">parameterName </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">@message</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">dbType </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">String</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">size </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">4000</span>&quot;<span style="color: blue">/&gt;
        &lt;</span><span style="color: #a31515">layout </span><span style="color: red">type</span><span style="color: blue">=</span>&quot;<span style="color: blue">log4net.Layout.PatternLayout</span>&quot; <span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">%message</span>&quot;<span style="color: blue">/&gt;
      &lt;/</span><span style="color: #a31515">parameter</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">appender</span><span style="color: blue">&gt;
    &lt;</span><span style="color: #a31515">root</span><span style="color: blue">&gt;
      &lt;</span><span style="color: #a31515">level </span><span style="color: red">value</span><span style="color: blue">=</span>&quot;<span style="color: blue">ERROR</span>&quot; <span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">appender-ref </span><span style="color: red">ref</span><span style="color: blue">=</span>&quot;<span style="color: blue">RollingLogFileAppender</span>&quot; <span style="color: blue">/&gt;
      &lt;</span><span style="color: #a31515">appender-ref </span><span style="color: red">ref</span><span style="color: blue">=</span>&quot;<span style="color: blue">ADONetAppender</span>&quot; <span style="color: blue">/&gt;
    &lt;/</span><span style="color: #a31515">root</span><span style="color: blue">&gt;
  &lt;/</span><span style="color: #a31515">log4net</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">configuration</span><span style="color: blue">&gt;
</span></pre>


<p>&#160;</p>

<p>&#160;</p>

<h2><font size="3"><font style="font-weight: bold">The code</font></font></h2>

<pre class="code"><span style="color: blue">public void </span>TestLog4NetPerformance()
{
    <span style="color: green">// Configure Log4Net based on de App.config settings.
    </span><span style="color: #2b91af">XmlConfigurator</span>.Configure();

    <span style="color: green">// Create a Log4Net logger object.
    </span><span style="color: #2b91af">ILog </span>_logger = <span style="color: #2b91af">LogManager</span>.GetLogger(<span style="color: #a31515">&quot;Testing Log4Net on Performance&quot;</span>);

    <span style="color: green">// Capture the start date and time
    </span><span style="color: #2b91af">DateTime </span>startDateTime = <span style="color: #2b91af">DateTime</span>.Now;

    <span style="color: green">// Set max for logging callss.
    </span><span style="color: blue">int </span>max = 100000000;
    <span style="color: blue">for </span>(<span style="color: blue">int </span>i = 0; i &lt; max; i++)
    {
        _logger.Debug(<span style="color: #a31515">&quot;This is a log4net debug log entry.&quot;</span>);
    }

    <span style="color: green">// Capture the end date and time
    </span><span style="color: #2b91af">DateTime </span>endDateTime = <span style="color: #2b91af">DateTime</span>.Now;

    <span style="color: green">// Calculate the time spent on logging.
    </span><span style="color: #2b91af">TimeSpan </span>duration = endDateTime - startDateTime;

    <span style="color: green">// Output to user
    </span><span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;Total duration in seconds: [{0}s]&quot;</span>, (<span style="color: blue">int</span>)duration.TotalSeconds));
}</pre>




<p><strong>The Results</strong></p>

<p><font color="#008000">1. [Root &gt; Level value=”ERROR”] – 100.000.000 – Total duration in seconds: [17s]</font></p>

<p>2. [threshold value=”ERROR”] – 100.000.000 – Total duration in seconds: [656s]</p>

<p>3. [LevelMatchFilter levelToMatch=”ERROR”] – 100.000.000 – Total duration in seconds: [716s]</p>

<p>4. [LevelRangeFilter levelMin=”ERROR” levelMax = ERROR] – 100.000.000 – Total duration in seconds: [715s]</p>

<p>&#160;</p>

<p>When a setting was used, all other settings where removed from the app.config.</p>

<p>&#160;</p>

<p><font size="4"><strong>So the winner is: Root &gt; Level!!!!!!</strong></font></p>
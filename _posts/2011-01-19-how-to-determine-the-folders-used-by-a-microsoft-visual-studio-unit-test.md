---
ID: 1882
post_title: >
  How to determine the folders used by a
  Microsoft Visual Studio unit test
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/01/19/how-to-determine-the-folders-used-by-a-microsoft-visual-studio-unit-test/
published: true
post_date: 2011-01-19 08:32:49
---
<p>You can use the directories used by a Microsoft Visual Studio unit test, by using the TestContext object.</p>  <pre class="code">[<span style="color: #2b91af">TestMethod</span>]
<span style="color: blue">public void </span>GetUnittestFolders()
{
    <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;CurrentTestOutcome [{0}]&quot;</span>, TestContext.CurrentTestOutcome));
    <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;DeploymentDirectory [{0}]&quot;</span>, TestContext.DeploymentDirectory));
    <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;ResultsDirectory [{0}]&quot;</span>, TestContext.ResultsDirectory));
    <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;TestDeploymentDir [{0}]&quot;</span>, TestContext.TestDeploymentDir));
    <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;TestDir [{0}]&quot;</span>, TestContext.TestDir));
    <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;TestLogsDir [{0}]&quot;</span>, TestContext.TestLogsDir));
    <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;TestRunDirectory [{0}]&quot;</span>, TestContext.TestRunDirectory));
    <span style="color: #2b91af">Console</span>.WriteLine(<span style="color: blue">string</span>.Format(<span style="color: #a31515">&quot;TestRunResultsDirectory [{0}]&quot;</span>, TestContext.TestRunResultsDirectory));
}</pre>

<p>&#160;</p>

<p>&#160;</p>

<p><strong>Result</strong></p>

<p>DeploymentDirectory [C:\Projects\ASF\Configurator\Main\TestResults\rLisdonk_L015 2011-01-19 08_27_21\Out]
  <br />ResultsDirectory [C:\Projects\ASF\Configurator\Main\TestResults\rLisdonk_L015 2011-01-19 08_27_21\In]

  <br />TestDeploymentDir [C:\Projects\ASF\Configurator\Main\TestResults\rLisdonk_L015 2011-01-19 08_27_21\Out]

  <br />TestDir [C:\Projects\ASF\Configurator\Main\TestResults\rLisdonk_L015 2011-01-19 08_27_21]

  <br />TestLogsDir [C:\Projects\ASF\Configurator\Main\TestResults\rLisdonk_L015 2011-01-19 08_27_21\In\L015]

  <br />TestRunDirectory [C:\Projects\ASF\Configurator\Main\TestResults\rLisdonk_L015 2011-01-19 08_27_21]

  <br />TestRunResultsDirectory [C:\Projects\ASF\Configurator\Main\TestResults\rLisdonk_L015 2011-01-19 08_27_21\In\L015]</p>
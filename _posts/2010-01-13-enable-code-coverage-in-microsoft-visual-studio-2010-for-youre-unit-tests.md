---
ID: 934
post_title: 'Enable Code Coverage in Microsoft Visual Studio 2010 for you&#8217;re unit tests'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/01/13/enable-code-coverage-in-microsoft-visual-studio-2010-for-youre-unit-tests/
published: true
post_date: 2010-01-13 08:55:17
---
<p>If you want to enable code coverage in Microsoft Visual Studio 2010 for you’re unit tests. Add a Test Project to you’re solution: File &gt; Add &gt; New Project… &gt; Visual C# &gt; Test &gt; Test Project.</p>  <p>This will automatically add the solution files “Local.testsettings”, “TestProject1.vsmdi” and “TraceAndTestImpact.testsettings”.   <br />    <br />Double click&#160; the “Local.testsettings” file &gt; Data and Diagnostics &gt; Check “Code Coverage”, then select the Code Coverage row and click on Configure    <br />    <br />&#160;<a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image3.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb3.png" width="606" height="330" /></a> </p>  <p>Check the assemblies you want the code coverage to be generated and click on OK.   <br />    <br />When you run you’re unit tests the code coverage will be generated (I added functions that are and are not covered by any unit tests to show the result)    <br />    <br /><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image4.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb4.png" width="603" height="415" /></a></p>
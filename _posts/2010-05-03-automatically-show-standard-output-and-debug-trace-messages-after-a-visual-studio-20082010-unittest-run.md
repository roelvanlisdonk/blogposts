---
ID: 1278
post_title: >
  Automatically show standard output and
  debug trace messages after a Visual
  Studio 2008/2010 UnitTest run
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/05/03/automatically-show-standard-output-and-debug-trace-messages-after-a-visual-studio-20082010-unittest-run/
published: true
post_date: 2010-05-03 11:17:50
---
<p>If you use the default settings of Microsoft Visual Studio 2008/2010 UnitTesting, the Console.WriteLine and Debug.WriteLine won’t be shown. By double clicking the test, you can see the test details, including the standard output and debug output, but I wanted to see the messages directly after a run. This can be done by right clicking de gridview in the Test Results window and adding the columns Output (StdOut) and Debug Trace.</p>  <p>&#160;</p>  <p><strong>UnitTest class</strong></p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Text;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>Microsoft.VisualStudio.TestTools.UnitTesting;

<span style="color: blue">namespace </span>Scripts
{
    [<span style="color: #2b91af">TestClass</span>]
    <span style="color: blue">public class </span><span style="color: #2b91af">MainUnitTest
    </span>{
        [<span style="color: #2b91af">TestMethod</span>]
        <span style="color: blue">public void </span>TestMethod1()
        {
            <span style="color: blue">string </span>result = <span style="color: blue">string</span>.Empty;

            result = <span style="color: #a31515">&quot;This is some debug output&quot;</span>;
            System.Diagnostics.<span style="color: #2b91af">Debug</span>.WriteLine(result);

            result = <span style="color: #a31515">&quot;This is some standard console output&quot;</span>;
            System.<span style="color: #2b91af">Console</span>.WriteLine(result);
        }
    }
}</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p><strong>Add columns</strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/05/image.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/05/image_thumb.png" width="754" height="323" /></a> </p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/05/image1.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/05/image_thumb1.png" width="404" height="376" /></a> </p>

<p>&#160;</p>

<p><strong>Test Result (showing standard console and debug output)</strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/05/image2.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/05/image_thumb2.png" width="754" height="207" /></a> </p>

<p>&#160;</p>

<p><strong>Details View</strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/05/image3.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/05/image_thumb3.png" width="754" height="238" /></a></p>
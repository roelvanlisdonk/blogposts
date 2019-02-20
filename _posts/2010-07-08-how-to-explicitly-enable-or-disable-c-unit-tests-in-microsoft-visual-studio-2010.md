---
ID: 1595
post_title: 'How to explicitly enable or disable C# unit tests in Microsoft Visual Studio 2010'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/07/08/how-to-explicitly-enable-or-disable-c-unit-tests-in-microsoft-visual-studio-2010/
published: true
post_date: 2010-07-08 09:54:54
---
<p>If you want to enable or disable unit tests in Microsoft Visual Studio 2010, you can use the “Ignore” attribute.</p>  <p>This can be used to ignore ore exclude integration tests in a nightly continuous integration build.</p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Text;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>Microsoft.VisualStudio.TestTools.UnitTesting;

<span style="color: blue">namespace </span>Rvl.Demo.Test
{
    [<span style="color: #2b91af">TestClass</span>]
    <span style="color: blue">public class </span><span style="color: #2b91af">UnitTest1
    </span>{
        [<span style="color: #2b91af">TestMethod</span>]
        [<span style="color: #2b91af">Ignore</span>]
        <span style="color: blue">public void </span>TestMethod1()
        {
            <span style="color: green">// This unit test will be excluded (ignored) from the test runs
        </span>}
    }
}</pre>
<a href="http://11011.net/software/vspaste"></a>
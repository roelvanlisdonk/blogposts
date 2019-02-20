---
ID: 724
post_title: >
  How to skip NUnit tests during
  continuous integration build
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/10/02/how-to-skip-nunit-tests-during-continuous-integration-build/
published: true
post_date: 2009-10-02 07:54:36
---
<p>Our continuous integration build server, runs all NUnit tests defined in a Microsoft Visual Studio solution file, but some NUnit tests are just created for integration testing. If you want to skip these tests you can use the NUnit attribute [Explicit]. These NUnit tests are only run when explicitly called from the nunit-console.exe command prompt. During the continuous integration build, these NUnit tests will be skipped.</p>  <pre class="code">        [<span style="color: #2b91af">Test</span>]
        [<span style="color: #2b91af">Explicit</span>(<span style="color: #a31515">&quot;Can't be run on build server, no IIS server on build server&quot;</span>)]
        <span style="color: blue">public void </span>IisIntegrationTest()
        {

        }</pre>
<a href="http://11011.net/software/vspaste"></a>
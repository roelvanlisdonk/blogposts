---
ID: 727
post_title: >
  Running specific NUnit tests to report
  only the coverage of a specific assembly
  with NCover
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/10/02/running-specific-nunit-tests-to-report-only-the-coverage-of-a-specific-assembly-with-ncover/
published: true
post_date: 2009-10-02 08:16:12
---
<p>If you have one NUnit test project per Microsoft Visual Studio solution, to test all the projects (assemblies) in the solution, running NCover on the NUnit test assembly, all NUnit tests will be run and the coverage of all assemblies will be reported, when you are just interested in a specific assembly, you can let NCover run only specific NUnit tests.   <br />This can be done in 2 ways:</p>  <p>- Specifying the namespace to test (in my case, preferable)   <br />- Using the NUnit attribute [Category]    <br />    <br /><strong>Specifying the namespace to test (in my case, preferable)     <br />      <br /></strong><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/10/image1.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/10/image_thumb1.png" width="615" height="382" /></a><strong>&#160; <br /></strong>In this way you don’t have to change you’re NUnit test code and because all NUnit tests of a specific assembly have a specific namespace, I can let NCover only run an report the coverage of a specific assemlby (subsystem).    <br /></p>  <p><strong>Using the NUnit [Category] attibute     <br /></strong>If you want to report the coverage of a specific group of NUnit tests, you can apply a category on the NUnit test in the group. NCover will only run and report the coverage of these NUnit tests.</p>  <pre class="code">        [<span style="color: #2b91af">Test</span>]
        [<span style="color: #2b91af">Category</span>(<span style="color: #a31515">&quot;MyCustomer.MyProduct.MySubsytem.MyCategory&quot;</span>)]
        <span style="color: blue">public void </span>TestForASpecificFunctionInASpecificAssemlby()
        {

        }</pre>
<a href="http://11011.net/software/vspaste"></a>

<p>In NCover you can report the coverage of this specific NUnit tests category by using the values:
  <br />

  <br />&#160;<a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/10/image.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2009/10/image_thumb.png" width="611" height="382" /></a></p>
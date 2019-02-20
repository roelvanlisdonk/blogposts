---
ID: 2573
post_title: >
  How to use content files from another
  project in a Visual Studio unit test, by
  using DeploymentItems.
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/03/13/how-to-use-content-files-from-an-other-project-in-a-visual-studio-unit-test-by-using-deploymentitems/
published: true
post_date: 2012-03-13 09:50:21
---
<p>&#160;</p>  <p>To access a file from another project in a Microsoft Visual Studio unit test, without specifying the absolute path, you can use DeploymentItems.</p>  <p>&#160;</p>  <p><strong>DeploymentItems</strong></p>  <p>DeploymentItems are files that will be copied to the output folder of the test. Microsoft Visual Studio tests are not run in the bin directory, but for each test a new directory is created, like: C:\Temp\Rli.Common\TestResults\rlisdonk_L084 2012-03-13 09_30_34\Out. DeploymentItems will be copied to this directory. </p>  <p>&#160;</p>  <p><strong>Enable DeploymentItems</strong></p>  <p>Double click on the Solution Item &gt; Local.testsettings in the Solution Explorer &gt; Click on Deployment &gt; check the &quot;Enable deployment&quot; checkbox &gt; Apply &gt; Close.</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image11.png" rel="lightbox"><img style="background-image: none; border-right-width: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image_thumb11.png" width="507" height="432" /></a></p>  <p>&#160;</p>  <p><strong>Add DeploymentItems</strong></p>  <p>Now you can add DeploymentItems to your TestClass or TestMethod:</p>  <pre class="code"><span style="color: blue">using </span>Microsoft.VisualStudio.TestTools.UnitTesting;

<span style="color: blue">namespace </span>Rli.TestProject
{
    [<span style="color: #2b91af">TestClass</span>]
    [<span style="color: #2b91af">DeploymentItem</span>(<span style="color: #a31515">@&quot;Rli.Common\Settings.xml&quot;</span>)]
    <span style="color: blue">public class </span><span style="color: #2b91af">UnitTest1
    </span>{
        [<span style="color: #2b91af">TestMethod</span>]
        <span style="color: blue">public void </span>TestMethod1()
        {
            <span style="color: #2b91af">Assert</span>.IsTrue(System.IO.<span style="color: #2b91af">File</span>.Exists(<span style="color: #a31515">&quot;Settings.xml&quot;</span>));
        }
    }
}</pre>

<p>The file [Settings.xml] in the Rli.Common project, can now be accessed in the unit test &quot;UnitTest1.TestMethod1&quot; in the Microsoft Visual Studio test project &quot;Rli.TestProject&quot;.</p>

<p>&#160;</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image12.png" rel="lightbox"><img style="background-image: none; border-right-width: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image_thumb12.png" width="580" height="249" /></a></p>

<p>&#160;</p>

<p>&#160;</p>

<p><strong>Notes</strong></p>

<ul>
  <li><strong>The relative path used in [<span style="color: #2b91af">DeploymentItem</span>(<span style="color: #a31515">@&quot;Rli.Common\Settings.xml&quot;</span>)]&#160; is relative to the Solution Folder!</strong></li>

  <li>If you want the file to be copied for all tests, you can add the file to the <strong>deployment files</strong> in the Local.testsettings. If you add the file to the deployment files, you don’t have to specify the DeploymetItem attribute on your TestClass or TestMethod, because the files will automatically be deploy to the test output folder:</li>

  <li><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image13.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image_thumb13.png" width="531" height="393" /></a></li>

  <li>If you only want to use a content file from another project, the test project does not have to reference the other project.</li>

  <li>Adding files as linked content files (Project &gt; Add Existing Item… &gt; browse to the file, select it and click on Add As Link) and <strong>setting the file property &quot;Copy to Output Directory&quot; property to &quot;Copy Always&quot; will not work in this case.</strong> <strong>You will need to use DeploymentItems</strong>. </li>

  <li>If you are using TFS with build templates, make sure the setting &quot;TestSettings File&quot; is set to a testsettings file that has Deployment files set to enabled. As testsettings file you can use, the Local.testsettings edited above.</li>
</ul>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image14.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image_thumb14.png" width="395" height="405" /></a></p>
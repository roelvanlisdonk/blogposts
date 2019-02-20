---
ID: 712
post_title: 'Debug you&#8217;re Microsoft Visual Studio 2008 setup project output msi with Debugger.break()'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/09/22/debug-youre-microsoft-visual-studio-2008-setup-project-output-msi-with-debugger-break/
published: true
post_date: 2009-09-22 09:29:16
---
<p>If you want to start the debugger after installation of you’re product with a Microsoft Visual Studio 2008 setup msi package, use a Installer class and custom actions and then add a Debugger.Break() on the AfterInstall event:   <br />    <br /></p>  <pre class="code">[<span style="color: #2b91af">RunInstaller</span>(<span style="color: blue">true</span>)]
    <span style="color: blue">public partial class </span><span style="color: #2b91af">ProjectInstaller </span>: <span style="color: #2b91af">Installer
    </span>{
        <span style="color: blue">public </span>ProjectInstaller()
        {
            InitializeComponent();
        }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Event fires after installation
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;sender&quot;&gt;&lt;/param&gt;
        /// &lt;param name=&quot;e&quot;&gt;&lt;/param&gt;
        </span><span style="color: blue">private void </span>AfterInstallation(<span style="color: blue">object </span>sender, <span style="color: #2b91af">InstallEventArgs </span>e)
        {
            <span style="color: #2b91af">Debugger</span>.Break();
        }
        <span style="color: gray">/// &lt;summary&gt;
        /// </span><span style="color: green">Event fires before uninstallation
        </span><span style="color: gray">/// &lt;/summary&gt;
        /// &lt;param name=&quot;sender&quot;&gt;&lt;/param&gt;
        /// &lt;param name=&quot;e&quot;&gt;&lt;/param&gt;
        </span><span style="color: blue">private void </span>BeforeUninstallation(<span style="color: blue">object </span>sender, <span style="color: #2b91af">InstallEventArgs </span>e)
        {

        }
    }</pre>
<a href="http://11011.net/software/vspaste"></a>
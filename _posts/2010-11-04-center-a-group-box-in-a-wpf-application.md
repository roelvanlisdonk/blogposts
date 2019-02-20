---
ID: 1801
post_title: Center a group box in a WPF application
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/11/04/center-a-group-box-in-a-wpf-application/
published: true
post_date: 2010-11-04 12:00:29
---
<p>If you want to center a group box in a WPF application, you can use the HorizontalAlignment property.</p>  <pre class="code"><span style="color: red">HorizontalAlignment</span><span style="color: blue">=&quot;Center&quot;
</span></pre>
<a href="http://11011.net/software/vspaste"></a>Make sure the margin left and margin right are 0

<p>&#160;</p>

<pre class="code"><span style="color: red">Margin</span><span style="color: blue">=&quot;0,30,0,0&quot;
</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/11/image2.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/11/image_thumb2.png" width="715" height="389" /></a> </p>

<p>&#160;</p>

<p><strong>Code</strong></p>

<pre class="code"><span style="color: blue">&lt;</span><span style="color: #a31515">Window </span><span style="color: red">x</span><span style="color: blue">:</span><span style="color: red">Class</span><span style="color: blue">=&quot;Rvl.DashBoard.Wpf.MainWindow&quot;
        </span><span style="color: red">xmlns</span><span style="color: blue">=&quot;http://schemas.microsoft.com/winfx/2006/xaml/presentation&quot;
        </span><span style="color: red">xmlns</span><span style="color: blue">:</span><span style="color: red">x</span><span style="color: blue">=&quot;http://schemas.microsoft.com/winfx/2006/xaml&quot;
        </span><span style="color: red">Title</span><span style="color: blue">=&quot;Dashboard&quot; </span><span style="color: red">Height</span><span style="color: blue">=&quot;350&quot; </span><span style="color: red">Width</span><span style="color: blue">=&quot;525&quot; </span><span style="color: red">WindowState</span><span style="color: blue">=&quot;Maximized&quot; </span><span style="color: red">Icon</span><span style="color: blue">=&quot;/Rvl.DashBoard.Wpf;component/Dashboard.ico&quot;&gt;
    &lt;</span><span style="color: #a31515">Grid</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">GroupBox </span><span style="color: red">Header</span><span style="color: blue">=&quot;Continuous Deployment&quot; </span><span style="color: red">Height</span><span style="color: blue">=&quot;107&quot; </span><span style="color: red">HorizontalAlignment</span><span style="color: blue">=&quot;Center&quot; </span><span style="color: red">Name</span><span style="color: blue">=&quot;continuousDeploymentGroupBox&quot; </span><span style="color: red">VerticalAlignment</span><span style="color: blue">=&quot;Top&quot; </span><span style="color: red">Width</span><span style="color: blue">=&quot;322&quot; </span><span style="color: red">HorizontalContentAlignment</span><span style="color: blue">=&quot;Center&quot; </span><span style="color: red">Margin</span><span style="color: blue">=&quot;0,30,0,0&quot;&gt;
            &lt;</span><span style="color: #a31515">Grid</span><span style="color: blue">&gt;
                &lt;</span><span style="color: #a31515">Button </span><span style="color: red">Content</span><span style="color: blue">=&quot;AKS&quot; </span><span style="color: red">Height</span><span style="color: blue">=&quot;23&quot; </span><span style="color: red">HorizontalAlignment</span><span style="color: blue">=&quot;Left&quot; </span><span style="color: red">Margin</span><span style="color: blue">=&quot;29,20,0,0&quot; </span><span style="color: red">Name</span><span style="color: blue">=&quot;aksButton&quot; </span><span style="color: red">VerticalAlignment</span><span style="color: blue">=&quot;Top&quot; </span><span style="color: red">Width</span><span style="color: blue">=&quot;75&quot; </span><span style="color: red">Click</span><span style="color: blue">=&quot;Deploy_AKS&quot; </span><span style="color: red">Cursor</span><span style="color: blue">=&quot;Hand&quot; /&gt;
                &lt;</span><span style="color: #a31515">Button </span><span style="color: red">Content</span><span style="color: blue">=&quot;LocatiePlatform&quot; </span><span style="color: red">Height</span><span style="color: blue">=&quot;23&quot; </span><span style="color: red">HorizontalAlignment</span><span style="color: blue">=&quot;Left&quot; </span><span style="color: red">Margin</span><span style="color: blue">=&quot;165,20,0,0&quot; </span><span style="color: red">Name</span><span style="color: blue">=&quot;locatiePlatformButton&quot; </span><span style="color: red">VerticalAlignment</span><span style="color: blue">=&quot;Top&quot; </span><span style="color: red">Width</span><span style="color: blue">=&quot;109&quot; </span><span style="color: red">Click</span><span style="color: blue">=&quot;Deploy_LocatiePlatform&quot; </span><span style="color: red">Cursor</span><span style="color: blue">=&quot;Hand&quot; /&gt;
            &lt;/</span><span style="color: #a31515">Grid</span><span style="color: blue">&gt;
        &lt;/</span><span style="color: #a31515">GroupBox</span><span style="color: blue">&gt;
    &lt;/</span><span style="color: #a31515">Grid</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">Window</span><span style="color: blue">&gt;

</span></pre>
<a href="http://11011.net/software/vspaste"></a>
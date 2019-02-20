---
ID: 1247
post_title: >
  Showing bmp, png, jpg or gif images as
  buttons in WPF in the best quality
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/04/19/showing-bmp-png-jpg-or-gif-images-as-buttons-in-wpf-in-the-best-quality/
published: true
post_date: 2010-04-19 21:39:45
---
<p>If you want to show a bmp, png, jpg or gif image as a button in WPF in the best quality, you can use the following XAML:</p>  <p>&#160;</p>  <p><strong>XAML</strong></p>  <pre class="code"><span style="color: blue">&lt;</span><span style="color: #a31515">Button  </span><span style="color: red">HorizontalAlignment</span><span style="color: blue">=&quot;Left&quot; </span><span style="color: red">Margin</span><span style="color: blue">=&quot;312,45,0,0&quot; </span><span style="color: red">Name</span><span style="color: blue">=&quot;refreshButton&quot; </span><span style="color: red">VerticalAlignment</span><span style="color: blue">=&quot;Top&quot; </span><span style="color: red">Width</span><span style="color: blue">=&quot;60&quot; </span><span style="color: red">Height</span><span style="color: blue">=&quot;45&quot; </span><span style="color: red">Cursor</span><span style="color: blue">=&quot;Hand&quot; </span><span style="color: red">Click</span><span style="color: blue">=&quot;button1_Click&quot;&gt;
  &lt;</span><span style="color: #a31515">Image </span><span style="color: red">Source</span><span style="color: blue">=&quot;/Ada.Tip.WpfUserControls;component/Images/SmallSync.png&quot; </span><span style="color: red">Stretch</span><span style="color: blue">=&quot;None&quot; /&gt;
&lt;/</span><span style="color: #a31515">Button</span><span style="color: blue">&gt;
</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p>* The Stretch property of the Image is set to “None”, so the image is shown in it’s original dimensions. If you let WPF scale the image you might not get the best quality. I use Paint .NET to scale the image to the correct size and then show the image in it’s original dimensions in WPF.</p>

<p>* Ada.Tip.WpfUserControls is the name of my Visual Studio 2010 project and assembly name.</p>

<p>&#160;</p>

<p>Add you’re image to the project and it will automatically be converted to a resource entry in you’re assembly</p>

<p>&#160;</p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/04/image21.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/04/image_thumb21.png" width="254" height="412" /></a> </p>

<p>&#160;</p>

<p><strong>Result (Refresh button)</strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/04/image22.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/04/image_thumb22.png" width="654" height="180" /></a></p>
---
ID: 1846
post_title: 'Setting 100% width and 100% height for a Textbox in WPF'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/12/09/setting-100-width-and-100-height-for-a-textbox-in-wpf/
published: true
post_date: 2010-12-09 13:07:01
---
<p>If you want to stretch a textbox to the width of the window in WPF you can use the following code</p>  <p>&#160;</p>  <p><strong>Code</strong></p>  <pre class="code"><span style="color: blue">&lt;</span><span style="color: #a31515">Window </span><span style="color: red">x</span><span style="color: blue">:</span><span style="color: red">Class</span><span style="color: blue">=&quot;Ada.Eac.UI.DeployWindow&quot;
        </span><span style="color: red">xmlns</span><span style="color: blue">=&quot;http://schemas.microsoft.com/winfx/2006/xaml/presentation&quot;
        </span><span style="color: red">xmlns</span><span style="color: blue">:</span><span style="color: red">x</span><span style="color: blue">=&quot;http://schemas.microsoft.com/winfx/2006/xaml&quot;
        </span><span style="color: red">Title</span><span style="color: blue">=&quot;DeployWindow&quot; </span><span style="color: red">Height</span><span style="color: blue">=&quot;300&quot; </span><span style="color: red">Width</span><span style="color: blue">=&quot;988&quot; </span><span style="color: red">SnapsToDevicePixels</span><span style="color: blue">=&quot;True&quot; </span><span style="color: red">UseLayoutRounding</span><span style="color: blue">=&quot;True&quot; </span><span style="color: red">WindowState</span><span style="color: blue">=&quot;Maximized&quot; </span><span style="color: red">WindowStartupLocation</span><span style="color: blue">=&quot;CenterScreen&quot; </span><span style="color: red">Icon</span><span style="color: blue">=&quot;/Eac;component/Dashboard.ico&quot;&gt;
    &lt;</span><span style="color: #a31515">Grid</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">Grid.ColumnDefinitions</span><span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">ColumnDefinition </span><span style="color: red">Width</span><span style="color: blue">=&quot;*&quot;&gt;&lt;/</span><span style="color: #a31515">ColumnDefinition</span><span style="color: blue">&gt;
        &lt;/</span><span style="color: #a31515">Grid.ColumnDefinitions</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">Grid.RowDefinitions</span><span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">RowDefinition </span><span style="color: red">Height</span><span style="color: blue">=&quot;60&quot;&gt;&lt;/</span><span style="color: #a31515">RowDefinition</span><span style="color: blue">&gt;
            &lt;</span><span style="color: #a31515">RowDefinition </span><span style="color: red">Height</span><span style="color: blue">=&quot;*&quot;&gt;&lt;/</span><span style="color: #a31515">RowDefinition</span><span style="color: blue">&gt;
        &lt;/</span><span style="color: #a31515">Grid.RowDefinitions</span><span style="color: blue">&gt;
        &lt;</span><span style="color: #a31515">Button </span><span style="color: red">Grid.Column</span><span style="color: blue">=&quot;1&quot; </span><span style="color: red">Content</span><span style="color: blue">=&quot;Deploy&quot; </span><span style="color: red">Height</span><span style="color: blue">=&quot;30&quot; </span><span style="color: red">Width</span><span style="color: blue">=&quot;100&quot; </span><span style="color: red">HorizontalAlignment</span><span style="color: blue">=&quot;Left&quot; </span><span style="color: red">Margin</span><span style="color: blue">=&quot;10,10,10,10&quot; </span><span style="color: red">Name</span><span style="color: blue">=&quot;deployButton&quot; </span><span style="color: red">Cursor</span><span style="color: blue">=&quot;Hand&quot; /&gt;
        &lt;</span><span style="color: #a31515">TextBox </span><span style="color: red">Grid.Column</span><span style="color: blue">=&quot;1&quot; </span><span style="color: red">Grid.Row</span><span style="color: blue">=&quot;2&quot;  </span><span style="color: red">HorizontalAlignment</span><span style="color: blue">=&quot;Stretch&quot; </span><span style="color: red">Name</span><span style="color: blue">=&quot;outputTextBox&quot; </span><span style="color: red">Margin</span><span style="color: blue">=&quot;10,10,10,10&quot; </span><span style="color: red">VerticalAlignment</span><span style="color: blue">=&quot;Stretch&quot; </span><span style="color: red">AcceptsReturn</span><span style="color: blue">=&quot;True&quot; </span><span style="color: red">VerticalScrollBarVisibility</span><span style="color: blue">=&quot;Auto&quot; /&gt;
    &lt;/</span><span style="color: #a31515">Grid</span><span style="color: blue">&gt;
&lt;/</span><span style="color: #a31515">Window</span><span style="color: blue">&gt;

</span></pre>
<a href="http://11011.net/software/vspaste"></a>

<p>&#160;</p>

<p>&#160;</p>

<p><strong>Screendump</strong></p>

<p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/12/image.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/12/image_thumb.png" width="493" height="367" /></a></p>
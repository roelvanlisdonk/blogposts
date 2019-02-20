---
ID: 1009
post_title: >
  Set focus to textbox in Microsoft
  Silverlight
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/01/28/set-focus-to-textbox-in-microsoft-silverlight/
published: true
post_date: 2010-01-28 10:16:23
---
<p>If you want to set the focus on a textbox in Microsoft Silverlight, use the Loaded event and the System.Windows.Browser.HtmlPage.Plugin.Focus() prior to calling Control.Focus()   <br />    <br /></p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Collections.Generic;
<span style="color: blue">using </span>System.Linq;
<span style="color: blue">using </span>System.Net;
<span style="color: blue">using </span>System.Windows;
<span style="color: blue">using </span>System.Windows.Controls;
<span style="color: blue">using </span>System.Windows.Documents;
<span style="color: blue">using </span>System.Windows.Input;
<span style="color: blue">using </span>System.Windows.Media;
<span style="color: blue">using </span>System.Windows.Media.Animation;
<span style="color: blue">using </span>System.Windows.Shapes;

<span style="color: blue">namespace </span>Ada.Tts.Toggle.Silverlight
{
  <span style="color: blue">public partial class </span><span style="color: #2b91af">MainPage </span>: <span style="color: #2b91af">UserControl
  </span>{
    <span style="color: gray">/// &lt;summary&gt;
    /// </span><span style="color: green">Event fires on page load
    </span><span style="color: gray">///
    /// </span><span style="color: green">Set focus to search box
    </span><span style="color: gray">/// &lt;/summary&gt;
    /// &lt;param name=&quot;sender&quot;&gt;&lt;/param&gt;
    /// &lt;param name=&quot;e&quot;&gt;&lt;/param&gt;
    </span><span style="color: blue">private void </span>UserControl_Loaded(<span style="color: blue">object </span>sender, <span style="color: #2b91af">RoutedEventArgs </span>e)
    {
      System.Windows.Browser.<span style="color: #2b91af">HtmlPage</span>.Plugin.Focus();
      <span style="color: blue">this</span>.searchTextBox.Focus();
    }
    <span style="color: gray">/// &lt;summary&gt;
    /// </span><span style="color: green">Consturctor
    </span><span style="color: gray">/// &lt;/summary&gt;
    </span><span style="color: blue">public </span>MainPage()
    {
      InitializeComponent();
    }
  }
}</pre>
<a href="http://11011.net/software/vspaste"></a>
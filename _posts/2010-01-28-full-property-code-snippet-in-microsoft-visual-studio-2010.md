---
ID: 1007
post_title: >
  Full property with backing field code
  snippet in Microsoft Visual Studio 2010
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/01/28/full-property-code-snippet-in-microsoft-visual-studio-2010/
published: true
post_date: 2010-01-28 10:04:42
---
<p>New in Microsoft Visual Studio 2010 is the “propfull” code snippet. It produces the code for a complete property with backing field.   <br />    <br />Press CTRL + spacebar and select [propfull], now press [Tab] once, this will generate the code.    <br />When you press [Tab] a second time you can change the type and name of the property.    <br />You can also directly type propfull in you’re editor and press [Tab].</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image33.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/01/image_thumb33.png" width="439" height="607" /></a> </p>  <p>&#160;</p>  <p>Generated code</p>  <pre class="code"><span style="color: blue">using </span>System;
<span style="color: blue">using </span>System.Net;
<span style="color: blue">using </span>System.Windows;
<span style="color: blue">using </span>System.Windows.Controls;
<span style="color: blue">using </span>System.Windows.Documents;
<span style="color: blue">using </span>System.Windows.Ink;
<span style="color: blue">using </span>System.Windows.Input;
<span style="color: blue">using </span>System.Windows.Media;
<span style="color: blue">using </span>System.Windows.Media.Animation;
<span style="color: blue">using </span>System.Windows.Shapes;

<span style="color: blue">namespace </span>Ada.Tts.Toggle.Silverlight
{
  <span style="color: blue">public class </span><span style="color: #2b91af">Task
  </span>{


    <span style="color: blue">private int </span>myVar;

    <span style="color: blue">public int </span>MyProperty
    {
      <span style="color: blue">get </span>{ <span style="color: blue">return </span>myVar; }
      <span style="color: blue">set </span>{ myVar = <span style="color: blue">value</span>; }
    }




  }
}</pre>
<a href="http://11011.net/software/vspaste"></a>
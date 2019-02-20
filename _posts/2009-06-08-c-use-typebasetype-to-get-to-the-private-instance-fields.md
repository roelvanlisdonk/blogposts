---
ID: 516
post_title: 'C# &#8211; Use Type.BaseType to get to the private instance fields'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/06/08/c-use-typebasetype-to-get-to-the-private-instance-fields/
published: true
post_date: 2009-06-08 09:53:32
---
<p>I used the Type.BaseType method to get to the private instance fields of a extended Microsoft ReportViewer Control.   <br />    <br /><span style="color: blue">public object </span>GetParametersArea(<span style="color: #2b91af">ExtendedReportViewer </span>viewer)    <br />{    <br /><span style="color: blue">&#160;&#160;&#160; return </span>viewer.GetType().BaseType.GetField(<span style="color: #a31515">&quot;m_parametersArea&quot;</span>, <span style="color: #2b91af">BindingFlags</span>.Instance | <span style="color: #2b91af">BindingFlags</span>.NonPublic).GetValue(viewer);    <br />}</p> You can't use the bindingflag option BindingFlags.FlattenHierarchy, because this option does not include private members (<a title="http://msdn.microsoft.com/en-us/library/6ztex2dc.aspx" href="http://msdn.microsoft.com/en-us/library/6ztex2dc.aspx">http://msdn.microsoft.com/en-us/library/6ztex2dc.aspx</a>)  <br />  <br />Solution found at: <a title="http://stackoverflow.com/questions/686482/c-accessing-inherited-private-instance-members-through-reflection" href="http://stackoverflow.com/questions/686482/c-accessing-inherited-private-instance-members-through-reflection">http://stackoverflow.com/questions/686482/c-accessing-inherited-private-instance-members-through-reflection</a>  <br /><a href="http://11011.net/software/vspaste"></a>
---
ID: 1080
post_title: >
  How to sett the RootVisual multiple
  times from code in Silverlight 3
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/03/09/how-to-sett-the-rootvisual-multiple-times-from-code-in-silverlight-3/
published: true
post_date: 2010-03-09 20:26:34
---
<p>MSDN explains the RootVisual can only be set one time from code:</p>  <p>   <br />You can set the value of the RootVisual property only one time from code, although you get its value any number of times.    <br /><a title="http://msdn.microsoft.com/en-us/library/system.windows.application.rootvisual(VS.95).aspx" href="http://msdn.microsoft.com/en-us/library/system.windows.application.rootvisual(VS.95).aspx">http://msdn.microsoft.com/en-us/library/system.windows.application.rootvisual(VS.95).aspx</a></p>  <p>   <br />But we can set it to a UserControl that can switch it’s own content, as explained in the blog post:</p>  <p><a title="http://craign.net/2008/03/11/how-to-switch-silverlight-usercontrols/" href="http://craign.net/2008/03/11/how-to-switch-silverlight-usercontrols/">http://craign.net/2008/03/11/how-to-switch-silverlight-usercontrols/</a></p>  <p>&#160;</p>  <p>I used this procedure to start with a progressIndicator and after authenticating the user and loading the user properties, showing the masterpage.</p>
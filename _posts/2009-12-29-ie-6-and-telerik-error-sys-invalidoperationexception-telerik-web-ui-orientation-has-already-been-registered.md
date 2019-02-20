---
ID: 898
post_title: 'IE 6 and Telerik error: Sys.InvalidOperationException Telerik.Web.UI.Orientation has already been registered'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/12/29/ie-6-and-telerik-error-sys-invalidoperationexception-telerik-web-ui-orientation-has-already-been-registered/
published: true
post_date: 2009-12-29 12:26:50
---
<p>If you get the error: <font color="#008000">Microsoft JScript runtime error: Sys.InvalidOperationException: Type Telerik.Web.UI.Orientation has already been registered. The type may be defined multiple times or the script file that defines it may have already been loaded. A possible cause is a change of settings during a partial update</font>. in IE 6, change the &lt;asp:ScriptManager in you’re master page to &lt;telerik:RadScriptManager</p>
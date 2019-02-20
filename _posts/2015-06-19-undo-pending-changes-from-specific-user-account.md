---
ID: 4420
post_title: >
  Undo pending changes from a specific
  user account
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/06/19/undo-pending-changes-from-specific-user-account/
published: true
post_date: 2015-06-19 13:48:09
---
<p>&#160;</p>  <p>If you want to undo some changes from a specific user, you can use:</p>  <p>&#160;</p>  <p>Change directory to folder containing &quot;tf.exe&quot;   <br />&#160;&#160;&#160; • cd &quot;C:\Program Files (x86)\Microsoft Visual Studio 12.0\Common7\IDE&quot;</p>  <p>   <br />Check the status of checked out files, to see correct &quot;account&quot;    <br />&#160;&#160;&#160; • tf status &quot;$/TFS/Path/To/Folder/To/Search/For/Pending/Changes&quot; /s:123.123.123.123 /u:* /recursive /format:detailed</p>  <p>   <br />Undo pending changes    <br />&#160;&#160;&#160; • tf undo /workspace:&quot;S001&quot;;MyDomain\myUserName &quot;$/TFS/Path/To/Folder/To/Search/For/Pending/Changes&quot; /recursive    </p>
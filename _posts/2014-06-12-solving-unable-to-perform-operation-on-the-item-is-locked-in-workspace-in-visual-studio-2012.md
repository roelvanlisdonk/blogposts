---
ID: 3837
post_title: 'Solving: Unable to perform operation on &#8230; The item &#8230; is locked in workspace &#8230; in Visual Studio 2012'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/06/12/solving-unable-to-perform-operation-on-the-item-is-locked-in-workspace-in-visual-studio-2012/
published: true
post_date: 2014-06-12 12:04:56
---
<p>&#160;</p>  <p>I wanted to check-in a file, that was check-out by myself on an other pc.</p>  <p>&#160;</p>  <p>You can revert those changes by using the tf.exe.</p>  <p>Open a command prompt AS ADMINISTRATOR</p>  <p>cd &quot;C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE&quot;</p>  <p align="left">tf undo /workspace:&quot;MYPC;MYDOMAIN\rlisdonk&quot; /collection:<a href="http://1.1.1.1:8080/tfs/MyCollection">http://1.1.1.1:8080/tfs/MyCollection</a> $/MyProduct/Main/Source/MyProject/Staging.cs</p>
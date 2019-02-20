---
ID: 535
post_title: 'msiexec exited on &#8216;server01&#8217; with error code 1605, when trying to remote install a msi package with psexec'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/06/11/msiexec-exited-on-server01-with-error-code-1605-when-trying-to-remote-install-a-msi-package-with-psexec/
published: true
post_date: 2009-06-11 12:29:18
---
<p>When trying to run a msi package on a remote server by using psexec, you can get the error 1605. This was caused by the “just me” button in the msi gui, during a manual installation. To force all msi packages to use the “Everyone” button, use ALLUSER=2   <br />    <br />psexec <a href="file://\\server01.test.nl">\\server01.test.nl</a> -u TEST\Administrator -p %password% msiexec /qn /i &quot;%ReleaseFolder%\Test.Setup.msi&quot; ALLUSERS=2    <br />    <br />Solution found at:    <br /><a title="http://www.cptloadtest.com/CategoryView,category,Tools.aspx" href="http://www.cptloadtest.com/CategoryView,category,Tools.aspx">http://www.cptloadtest.com/CategoryView,category,Tools.aspx</a>    <br />    <br />More on psexec: <a title="http://forum.sysinternals.com/forum_posts.asp?TID=15920" href="http://forum.sysinternals.com/forum_posts.asp?TID=15920">http://forum.sysinternals.com/forum_posts.asp?TID=15920</a></p>
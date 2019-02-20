---
ID: 4277
post_title: >
  Move C:\ProgramData\Package Cache\ to
  D:\
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/02/27/move-cprogramdatapackage-cache-to-d/
published: true
post_date: 2015-02-27 08:50:58
---
<p>Windows with a couple of development tools takes up about 126GB of my 128GB SSD, to free-up some space I followed the guide at: <a title="http://www.hanselman.com/blog/GuideToFreeingUpDiskSpaceUnderWindows81.aspx" href="http://www.hanselman.com/blog/GuideToFreeingUpDiskSpaceUnderWindows81.aspx">http://www.hanselman.com/blog/GuideToFreeingUpDiskSpaceUnderWindows81.aspx</a></p>  <p>&#160;</p>  <p>Then I moved the &quot;C:\ProgramData\Package Cache&quot; used by Visual Studio to D:\.</p>  <p>&#160;</p>  <p>I did this by following the instructions at: <a title="http://superuser.com/questions/455853/can-i-delete-the-the-folder-c-programdata-package-cache" href="http://superuser.com/questions/455853/can-i-delete-the-the-folder-c-programdata-package-cache">http://superuser.com/questions/455853/can-i-delete-the-the-folder-c-programdata-package-cache</a></p>  <p>&#160;</p>  <p>1. Move folder from C:\ProgramData to D:\ProgramData</p>  <p>This must be a <strong>move</strong> of the complete “Package Cache” folder, so after move you will have a folder C:\ProgramData, that does NOT contain the folder “Package Cache”.</p>  <p>2. Create a filesystem junction: mklink /J &quot;C:\ProgramData\Package Cache&quot; &quot;D:\ProgramData\Package Cache&quot;</p>  <p>This will create a filesystem junction, that will point all software that wants to access&#160; &quot;C:\ProgramData\Package Cache&quot; to &quot;D:\ProgramData\Packa Cache&quot;.</p>  <p>&#160;</p>  <p>That alone saved me about 6GB.</p>
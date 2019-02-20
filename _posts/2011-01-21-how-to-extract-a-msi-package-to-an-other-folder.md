---
ID: 1884
post_title: 'How to extract a *.msi package to an other folder'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/01/21/how-to-extract-a-msi-package-to-an-other-folder/
published: true
post_date: 2011-01-21 14:22:05
---
<p>If you want to extract an *.msi package to a specific folder, use:   <br />    <br />    <br />msiexec /a Example.msi TARGETDIR=&quot;C:\Temp\Program Files&quot; /qn    <br />    <br />This will extract the contents of the Example.msi to a folder &quot;C:\Temp\Program Files&quot;    </p>
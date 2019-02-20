---
ID: 462
post_title: >
  VMWare Workstation 6 some remote file
  systems do not support files larger than
  2 GB, solution
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/05/22/vmware-workstation-6-some-remote-file-systems-do-not-support-files-larger-than-2-gb-solution/
published: true
post_date: 2009-05-22 15:30:59
---
<p>When you open an *.vmx file larger then 2GB from an UNC path, you will get an error    <br />&#8230;     <br />Some remote file systems do not support files larger than 2GB     <br />&#8230;     <br />Adding <strong>diskLib.sparseMaxFileSizeCheck= &quot;FALSE&quot;</strong> in the *.vmx file solved the problem.</p>
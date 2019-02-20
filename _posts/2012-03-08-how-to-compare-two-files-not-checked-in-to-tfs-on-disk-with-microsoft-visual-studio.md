---
ID: 2544
post_title: >
  How to compare two files (not checked in
  to TFS) on disk with Microsoft Visual
  Studio
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/03/08/how-to-compare-two-files-not-checked-in-to-tfs-on-disk-with-microsoft-visual-studio/
published: true
post_date: 2012-03-08 08:53:31
---
<p>If you want to compare two files on disk that are not checked in to TFS, by using Microsoft Visual Studio, you can use the following steps:</p>  <p>1. Open Microsoft Visual Studio &gt; Team Explorer &gt; Source Control</p>  <p>2. Navigate to a random file en right click it:</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image7.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image_thumb7.png" width="254" height="341" /></a></p>  <p>3. Click on Compare…</p>  <p>4. For the Source Path: Click Browse… &gt; Local Path… and browse to the first file.</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image8.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2012/03/image_thumb8.png" width="452" height="265" /></a></p>  <p>5. Repeat this for the target path</p>  <p>6. Click OK</p>  <p>&#160;</p>  <p>Now the two files will be compared and the differences will be shown, without the files being checked in to TFS.</p>
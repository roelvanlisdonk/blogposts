---
ID: 2010
post_title: >
  Solving:Locked / checked out files in
  TFS 2010 on an other workspace
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/05/06/solvinglocked-checked-out-files-in-tfs-2010-on-an-other-workspace/
published: true
post_date: 2011-05-06 15:38:06
---
<p>When you use different (virtual) machines to check out files in Microsoft TFS 2010, different workspaces are used. If you forget to check in a file on machine A, you can’t check that specific in on machine B. To solve this problem there are multiple solutions:</p>  <p>1. Start machine A en check the files in.</p>  <p>2. Use the TFS administration application if you have sufficient rights.</p>  <p>or</p>  <p>3. Delete the machine A workspace in the Source Control Explorer on Machine B.</p>  <p>&#160;</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image1.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image_thumb1.png" width="545" height="74" /></a></p>  <p>Delete workspace:</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image2.png" rel="lightbox"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2011/05/image_thumb2.png" width="488" height="369" /></a></p>    <p>After deleting the workspace I could check the files out and in again.</p>
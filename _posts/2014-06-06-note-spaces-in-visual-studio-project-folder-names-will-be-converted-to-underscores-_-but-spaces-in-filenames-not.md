---
ID: 3825
post_title: 'Note: Spaces in Visual Studio project folder names will be converted to underscores (&quot;_&quot;) in embeded resouce name, but spaces in filenames not.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/06/06/note-spaces-in-visual-studio-project-folder-names-will-be-converted-to-underscores-_-but-spaces-in-filenames-not/
published: true
post_date: 2014-06-06 14:38:10
---
&nbsp;

If you have an embedded resource file, like:

&nbsp;

<a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/06/image5.png" rel="lightbox"><img style="background-image: none; padding-top: 0px; padding-left: 0px; margin: 0px 5px; display: inline; padding-right: 0px; border: 0px;" title="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2014/06/image_thumb5.png" alt="image" width="376" height="142" border="0" /></a>

&nbsp;

The embedded resource filename will be:

&nbsp;

Research.UnitTests.<span style="color: #0000ff;">Folder_path_with_spaces</span>.<span style="color: #f79646;">Text file with spaces.txt</span>

&nbsp;

The spaces in the foldername will be replaced by underscores ("_"), see <span style="color: #0000ff;">Folder_path_with_spaces</span> .

But the filename will contain spaces, see <span style="color: #f79646;">Text file with spaces.txt</span>
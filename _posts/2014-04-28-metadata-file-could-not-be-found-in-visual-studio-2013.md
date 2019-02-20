---
ID: 3745
post_title: >
  Metadata file could not be found in
  Visual Studio 2013
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/04/28/metadata-file-could-not-be-found-in-visual-studio-2013/
published: true
post_date: 2014-04-28 13:29:52
---
<p>I was getting the error “Metadata file could not be found” in Microsoft Visual Studio 2013, normally I would clean the solution and build the projects in the correct order manually, but that did not fix the problem.</p>  <p>&#160;</p>  <p>After removing the *.suo file, (with the same name as the solution) the problem was resolved.</p>
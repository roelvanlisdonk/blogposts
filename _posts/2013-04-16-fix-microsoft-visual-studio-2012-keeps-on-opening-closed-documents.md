---
ID: 3202
post_title: 'Fix: Microsoft Visual Studio 2012 keeps on opening closed documents'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2013/04/16/fix-microsoft-visual-studio-2012-keeps-on-opening-closed-documents/
published: true
post_date: 2013-04-16 08:39:29
---
<p>When I closed all documents (tabs), closed en reopened Microsoft Visual Studio 2012 some closed documents were reopened again. After deleting the *.suo files in the same folder as the *.sln file, this problem was fixed.</p>
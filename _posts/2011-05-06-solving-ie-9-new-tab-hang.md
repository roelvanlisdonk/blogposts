---
ID: 2005
post_title: Solving IE 9 new tab hang
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2011/05/06/solving-ie-9-new-tab-hang/
published: true
post_date: 2011-05-06 13:26:30
---
<p align="left">After you install a very old version of the SourceGear Vault client (v3.1.9.3798), opening a link in a new tab in IE 9 will hang that new tab. This is caused by the SourceGear Vault isntaller, overwriting some registry settings. I posted a similar problem on IE 8 [<a title="http://www.roelvanlisdonk.nl/?p=871" href="http://www.roelvanlisdonk.nl/?p=871">http://www.roelvanlisdonk.nl/?p=871</a>], but that fix, did not fix the problem in IE 9.</p>  <p align="left">&#160;</p>  <p align="left">I found my solution on: <a title="http://iefaq.info/index.php?action=artikel&amp;;cat=42&amp;id=133&amp;artlang=en" href="http://iefaq.info/index.php?action=artikel&amp;;cat=42&amp;id=133&amp;artlang=en">http://iefaq.info/index.php?action=artikel&amp;;cat=42&amp;id=133&amp;artlang=en</a></p>  <p>Running the [ie8-rereg.all] fixed my problem.</p>
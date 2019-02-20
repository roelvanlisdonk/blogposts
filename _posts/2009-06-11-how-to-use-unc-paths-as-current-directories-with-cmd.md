---
ID: 537
post_title: >
  How to use UNC paths as current
  directories with cmd
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2009/06/11/how-to-use-unc-paths-as-current-directories-with-cmd/
published: true
post_date: 2009-06-11 13:14:22
---
<p>When you enter cd “\\myserver\myshare” in het cmd.exe dialog, you get the error CMD does not support UNC paths as current directories. But what if you want to run a bat file from a networkshare and use that share as the current directory, you can use cmd.exe but you will have to use pushd and when done use popd, this will automatically mount a drive to the given network share, so you can use the network share as current directory:   <br />    <br />C:\pushd <a href="file://\\myserver\myshare">\\myserver\myshare</a>    <br />C:\popd    </p>
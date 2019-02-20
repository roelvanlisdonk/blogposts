---
ID: 2649
post_title: 'How to hide the command line window, when started from an other batch (*.cmd or *.bat) file.'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/04/10/how-to-hide-the-command-line-window-when-started-from-an-other-batch-cmd-or-bat-file/
published: true
post_date: 2012-04-10 15:53:34
---
<p>If you want to start a batch file from an other batch file you can use the start command.</p>  <p>If you want to hide the command line window, that will be displayed by default, use the /B parameter.</p>  <p>&#160;</p>  <p>Example</p>  <p>Test1.bat contents:</p>  <p>start /B /wait Test2.bat</p>  <p>exit</p>  <p>&#160;</p>  <p>When you execute Test1.bat on the command line, the Test2.bat will be executed without showing a window.</p>  <p>(The Test1.bat will wait until Test2.bat is finished, because the /wait argument is supplied.)</p>
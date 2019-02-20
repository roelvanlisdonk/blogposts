---
ID: 4796
post_title: 'Fix: ECMDERR Failed to execute &quot;git ls-remote &#8211;tags &#8211;heads git://github.com/systemjs/systemjs.git&quot;, exit code of #128'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2016/01/18/fix-ecmderr-failed-to-execute-git-ls-remote-tags-heads-gitgithub-comsystemjssystemjs-git-exit-code-of-128/
published: true
post_date: 2016-01-18 14:53:18
---
<p>When I wanted to install a bower package inside Microsoft Visual Studio 2015 update 1 (inside a corporate netwerok), I got the error:</p>  <p>ECMDERR Failed to execute &quot;git ls-remote --tags --heads git://github.com/systemjs/systemjs.git&quot;, exit code of #128</p>  <p>&#160;</p>  <p>This solution: <a title="http://stackoverflow.com/questions/21789683/how-to-fix-bower-ecmderr" href="http://stackoverflow.com/questions/21789683/how-to-fix-bower-ecmderr">http://stackoverflow.com/questions/21789683/how-to-fix-bower-ecmderr</a></p>  <p>Enter the following command on the commandline:</p>  <p><strong>git config --global url.&quot;</strong><a href="https://&quot;.insteadOf"><strong>https://&quot;.insteadOf</strong></a><strong> git://</strong></p>
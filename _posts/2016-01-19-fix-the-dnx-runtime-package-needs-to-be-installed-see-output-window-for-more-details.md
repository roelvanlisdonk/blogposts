---
ID: 4799
post_title: 'Fix: The Dnx Runtime package needs to be installed. See output window for more details'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2016/01/19/fix-the-dnx-runtime-package-needs-to-be-installed-see-output-window-for-more-details/
published: true
post_date: 2016-01-19 13:50:46
---
<p>I do not know what caused the problem, but at a given moment, I got the error: </p>  <p>&#160;</p>  <p><a href="http://stackoverflow.com/questions/31957824/the-dnx-runtime-package-needs-to-be-installed-see-output-window-for-more-detail">The Dnx Runtime package needs to be installed. See output window for more details</a></p>  <p>&#160;</p>  <p>To fix this problem I entered the following commands in the package manager console:</p>  <p>&#160;</p>  <p>dnvm upgrade</p>  <p>dnvm upgrade –r CoreClr</p>  <p>dnu restore</p>  <p>&#160;</p>  <p>Closed all visual studio 2015 instances and opened the project,&#160; now I could build the project wihout errors.</p>  <p>&#160;</p>  <p align="left">Found my solution at: <a title="http://stackoverflow.com/questions/31957824/the-dnx-runtime-package-needs-to-be-installed-see-output-window-for-more-detail" href="http://stackoverflow.com/questions/31957824/the-dnx-runtime-package-needs-to-be-installed-see-output-window-for-more-detail">http://stackoverflow.com/questions/31957824/the-dnx-runtime-package-needs-to-be-installed-see-output-window-for-more-detail</a></p>
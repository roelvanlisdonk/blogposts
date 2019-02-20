---
ID: 1040
post_title: 'How to resolve: SSIS package won&#8217;t stop debugger on script task'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2010/02/19/how-to-resolve-ssis-package-wont-stop-debugger-on-script-task/
published: true
post_date: 2010-02-19 14:35:54
---
<p>When you are on a x64 machine and de business intellegence studio doesn’t stop the debugger in you’re script task on the break points, set you’re package to x86 (Run64BitRuntime = False) to start debugging the package.</p>  <p><a href="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/02/image9.png"><img style="border-bottom: 0px; border-left: 0px; display: inline; border-top: 0px; border-right: 0px" title="image" border="0" alt="image" src="http://www.roelvanlisdonk.nl/wp-content/uploads/2010/02/image_thumb9.png" width="649" height="401" /></a> </p>  <p>Make sure the package is selected en not the individual task (then the debugger also won’t stop).</p>
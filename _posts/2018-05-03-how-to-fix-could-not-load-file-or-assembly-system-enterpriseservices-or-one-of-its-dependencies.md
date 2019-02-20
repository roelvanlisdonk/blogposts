---
ID: 5162
post_title: 'How to fix: Could not load file or assembly &#8216;System.EnterpriseServices&#8217; or one of its dependencies'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2018/05/03/how-to-fix-could-not-load-file-or-assembly-system-enterpriseservices-or-one-of-its-dependencies/
published: true
post_date: 2018-05-03 09:18:04
---
<p>
 </p><p>An old ASP .NET 32-bit web application would not start, when reinstalled on a new machine:
</p><p><span style="color:black; font-size:12pt">Could not load file or assembly 'System.EnterpriseServices' or one of its dependencies. An attempt was made to load a program with an incorrect format. 
</span></p><p><span style="color:black; font-size:12pt">Description: An unhandled exception occurred during the execution of the current web request. Please review the stack trace for more information about the error and where it originated in the code. 
</span></p><p><span style="color:black; font-size:12pt"> Exception Details: System.BadImageFormatException: Could not load file or assembly 'System.EnterpriseServices' or one of its dependencies. An attempt was made to load a program with an incorrect format.
</span></p><p>
 </p><p><span style="color:black; font-size:12pt">To fix this problem, I just had to enable 32-bits applications on the application pool (Advanced Settings):
</span></p><p>
 </p><p><img src="https://www.roelvanlisdonk.nl/wp-content/uploads/2018/05/050318_0718_HowtofixCou1.png" alt=""/></p>